---
title: Docker Compose
layout: post
subtitle: 프로젝트에 Docker Compose 적용하기
tags:
- docker
- devops
author: Jeongsu Yang
comments: 'True'
---

## Docker Compose 개요

### Docker Compose 란

- 다중 컨테이너 Docker 애플리케이션을 정의하고 실해하기 위한 도구입니다.
- YAML 파일을 사용하여 응용 프로그램 서비스를 구성합니다.
- 기본적으로 3단계의 프로세스로 실행:
  1. **Dockerfile 파일 정의**: 애플리케이션의 실행환경을 정의한다. 어디에서나 동일한 환경의 재현이 가능합니다.
  2. **docker-compose.yml 파일 정의**: 앱을 구성하는 서비스가 격리된 환경에서 함께 실행될 수 있도록 정의합니다.
  3. **docker-compose up 실행**: 전체 앱을 시작하고 실행한다.

### Docker Compose 주요 명령어

#### up

- docker-compose.yml 파일의 내용에 따라 이미지를 빌드하고 서비스를 실행합니다.
  1. 서비스를 띄울 네트워크 설정
  2. 필요한 볼륨 생성
  3. 필요한 이미지 pull
  4. 필요한 이미지 build
  5. 서비스 의존성에 따라 서비스 실행

```
$ docker-compose up -d
Creating network "myrecipes-api_default" with the default driver
Creating rabbitmq ... done
Creating mongo    ... done
Creating redis    ... done
```

#### down

- 서비스를 지웁니다. 컨테이너와 네트워크를 삭제하며, 옵션에 따라 볼륨도 지웁니다.

```
$ docker-compose down
Removing redis    ... done
Removing mongo    ... done
Removing rabbitmq ... done
Removing network myrecipes-api_default
```

#### start

- 서비스를 시작합니다.

```
$ docker-compose start
Starting redis    ... done
Starting rabbitmq ... done
Starting mongo    ... done
```

#### stop

- 서비스를 중지합니다.

```
$ docker-compose stop
Stopping redis    ... done
Stopping mongo    ... done
Stopping rabbitmq ... done
```

#### ps

- 현재 환경에서 실행 중인 서비스를 보여줍니다.

```
$ docker-compose ps
  Name                Command                       State                                                                           Ports                                                                
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
mongo      docker-entrypoint.sh mongod      Up (health: starting)   0.0.0.0:27017->27017/tcp                                                                                                             
rabbitmq   docker-entrypoint.sh rabbi ...   Up (health: starting)   15671/tcp, 0.0.0.0:15672->15672/tcp, 0.0.0.0:25672->25672/tcp, 0.0.0.0:4369->4369/tcp, 0.0.0.0:5671->5671/tcp, 0.0.0.0:5672->5672/tcp
redis      docker-entrypoint.sh redis ...   Up (health: starting)   0.0.0.0:6379->6379/tcp
```

#### exec

- 실행 중인 컨테이너에서 명령을 실행합니다.

```
$ docker-compose exec rabbitmq rabbitmq-plugins enable rabbitmq_management
...
```


#### logs

- 서비스의 로그를 확인할 수 있습니다.

```
$ docker-compose logs rabbitmq
Attaching to rabbitmq
rabbitmq    | 2020-02-06 06:47:54.001 [info] <0.8.0> Feature flags: list of feature flags found:
...
```

##  API 프로젝트에 Docker Compose 적용하기

### 적용하게 된 계기

- API 서비스가 정상으로 실행되려면 몇가지 서비스가 함께 실행되어 있어야 합니다.
- docker 명령을 통해서 컨테이너를 실행하는 것이 가능하지만, 한개씩 컨테이너를 실행해야 되기 때문에 불편합니다.
- API 서비스를 실행하기 전에 docker-compose 명령으로 필요한 서비스를 한번에 실행할 수 있습니다.

### 적용하기

**1. docker-compose.yml 파일 정의**
  - Redis, RabbitMQ, MongoDB 서비스를 docker-compose.yml 파일에 정의합니다.
  - RabbitMQ는 콘솔 접근을 가능하게 하기 위해서 관리 플러그인이 활성화되어 있는 rabbitmq:3-management 이미지를 사용했습니다.
  - 콘솔 기본 사용자와 비밀번호 수정을 위해서 환경변수 설정을 하였습니다.

```
version: '3'

services:
  redis:
    container_name: redis
    image: redis:latest
    ports:
      - "6379:6379"
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 30s
      timeout: 10s
      retries: 5
  rabbitmq:
    container_name: rabbitmq
    image: rabbitmq:3-management
    ports:
      - "4369:4369"
      - "5671-5672:5671-5672"
      - "15672:15672"
      - "25672:25672"
    environment:
      - RABBITMQ_DEFAULT_USER=rabbitmq
      - RABBITMQ_DEFAULT_PASS=qwer1234!
    healthcheck:
      test: ["CMD-SHELL", "if rabbitmqctl status; then \nexit 0 \nfi \nexit 1"]
      interval: 30s
      timeout: 10s
      retries: 5
  mongo:
    container_name: mongo
    image: mongo:latest
    ports:
      - "27017:27017"
    healthcheck:
      test: ["CMD", "mongo",  "--eval", "db.adminCommand('ping')"]
      interval: 30s
      timeout: 10s
      retries: 5
```

**2. 서비스 실행**
  - docker-compose up 명령을 실행하여 정의한 서비스들을 실행합니다.

**3. API 서비스 실행**
  - 필요한 서비스들이 실행되어 있기 때문에 정상 동작합니다.

### 아쉬운 점

- API 서비스는 별도로 실행해야 되서 한번에 실행이 불가능합니다.
  - docker-compose.yml 파일에 API 서비스도 함께 정의할 예정입니다.