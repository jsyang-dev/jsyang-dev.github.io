---
layout: post
title: MY.레시피 프로젝트 소개
subtitle : 프로젝트 소개 및 내용
tags: [Project, Java, Spring Boot, Study]
author: Jeongsu Yang
comments : True
---

## 프로젝트 소개

![screenshot](/assets/project/front-screenshot.jpg)

<br>

### 프로젝트 목적

* MY.레시피는 레시피를 등록하여 공유할 수 있는 사이트입니다.
* 본 프로젝트는 개발하면서 새로운 기술들을 공부하고 적용하고자 사이드 프로트로 진행하고 있습니다.
* 나만의 개발 표준을 정하고, 이를 지키면서 코딩하기 위해 노력하고 있습니다.
* 일과 육아와 공부를 병행하기 위해서 매일 저녁에 적어도 1시간 이상 코딩을 하고 있습니다.

<br>

### 프로젝트 기간

* 2019.9 ~ 진행중

<br>

### 프로젝트 구성도

![diagram](/assets/project/diagram.png)

<br>

### 프로젝트 설명

*  myrecipes-front: 프런트 페이지 제공을 위한 프로젝트
*  myrecipes-api: 레시피, 회원 관련 API를 제공하는 프로젝트
*  system-api: 로그 관련 API를 제공하는 프로젝트
*  myrecipes-batch: 배지 작업을 위한 프로젝트
*  myrecipes-admin: 어드민 페이지 제공을 위한 프로젝트(향후 개발 예정)

<br>

### 데모 사이트 

* [http://service.myrecipes.link:8080/](http://service.myrecipes.link:8080/)

<br>

## 사용기술

### 데이터베이스

* MySQL: 트랜잭션 데이터 저장을 위한 데이터베이스
* MongoDB: 로그 데이터 저장, 빠른 응답속도가 보장되어야 하는 데이터(ex: 메인페이지 인기레시피 리스트)

<br>

### Spring 라이브러리

* Spring Thymeleaf: 프런트 웹페이지 구성을 위한 템플릿 엔진
* Spring Security: 인증과 인가, CSRF 방지와 같은 보안 적용
* Spring Data JPA: 관계형 데이터베이스를 JPA로 객체지향적으로 사용
* Spring Data Redis: 캐싱을 위한 Redis 사용
* Spring AOP: 전체 메소드를 대상으로 호출 및 실패 로그를 RabbitMQ로 보내기 위해 사용
* Spring AMQP: RabbitMQ에 메시지를 생산하고 소비하기 위해 사용

<br>

### 오픈소스

* Jenkins: CICD 구성을 위해 사용
* Redis: Service 레이어에서 결과 캐싱을 위해 사용
* RabbitMQ: 대량의 로그 데이터를 유실없이 전달하기 위해 사용

<br>

### 기타

* Docker: 프로젝트를 컨테이너로 배포
* SonarCloud: 프로젝트 분석과 커버리지 결과를 제공, 잠재적인 보안 위협이나 기술 부채를 제거
* Slack: Jenkins에서 이벤트 발생 시 알람
* AWS(EC2, S3): 배포 인프라, 정적 리소스 저장을 위한 용도

<br>
