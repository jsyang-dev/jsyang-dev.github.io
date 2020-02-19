---
title: Kubernetes
layout: post
subtitle: Kubernetes에 Spring Boot 프로젝트 배포하기
tags:
- Kubernetes
- devops
author: Jeongsu Yang
comments: 'True'
---

## Kubernetes 개요

### Kubernetes 란

- 컨테이너를 쉽고 빠르게 배포/확장하고 관리를 자동화해주는 오픈소스 플랫폼

### MacOS에 Kubernetes 설치

### 대시보드 설치

### Docker Hub 가입하기

## Kubernetes에 Spring Boot 프로젝트 배포하기

### Dockerfile 생성

- 프로젝트 루트에 Dockerfile을 생성합니다.

```dockerfile
FROM openjdk:11-jdk-slim
COPY target/*.jar app.jar
CMD ["java", "-XX:+UseG1GC", "-XX:MaxMetaspaceSize=512m", "-XX:MetaspaceSize=256m", "-jar", "app.jar"]
```

### 프로젝트 빌드

- 애플리케이션을 빌드해서 jar 파일을 생성합니다.

```bash
# Maven 프로젝트
./mvnw clean package

# Gradle 프로젝트
./gradlew clean build
```

### Docker 이미지 빌드

- Dockerfile이 있는 루트에서 실행하여 Docker 이미지를 생성합니다.

```bash
docker build -t mycat83/sample .
```

- 빌드 성공 후 아래 명령어를 실행하여 이미지가 정상적으로 생성되었는지 확인이 가능합니다.

```bash
docker images
```

### Docker 이미지 푸시

- Docker Hub에 로그인 합니다.

```bash
docker login
```

- 생성된 Docker 이미지를 Docker Hub에 푸시합니다.

```bash
docker push mycat83/sample
```

### Kubernetes에 배포

- 아래 명령어 3개를 실행하여 배포를 deployment.yml 파일을 생성합니다.

```bash
kubectl create deployment sample --image=mycat83/sample --dry-run -o=yaml > deployment.yml

echo --- >> deployment.yml

kubectl create service clusterip sample --tcp=8080:8080 --dry-run -o=yaml >> deployment.yml
```

- 생성된 deployment.yml 파일

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: sample
  name: sample
spec:
  replicas: 1
  selector:
    matchLabels:
      app: sample
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: sample
    spec:
      containers:
      - image: mycat83/sample
        name: sample
        resources: {}
status: {}
---
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: sample
  name: sample
spec:
  ports:
  - name: 8080-8080
    port: 8080
    protocol: TCP
    targetPort: 8080
  selector:
    app: sample
  type: ClusterIP
status:
  loadBalancer: {}
```

- 배포를 위해 명령어를 수행합니다.

```bash
kubectl apply -f deployment.yaml
```

### 배포된 애플리케이션 확인

- 대시보드 확인

- 포트 포워딩을 사용해서 애플리케이션에 접근합니다.

```bash
kubectl port-forward svc/sample 8080:8080
```
