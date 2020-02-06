---
title: 디자인 패턴 - Singleton
layout: post
subtitle: 인스턴스를 한 개만 만들기
tags:
- java
- designpattern
author: Jeongsu Yang
comments: 'True'
---

## Singleton 패턴

### 정의

* 인스턴스가 한 개밖에 존재하지 않는 것을 보증하는 패턴을 Singlton 패턴이라고 한다.

### 사용 목적

* 인스턴스가 1개밖에 없다라는 전제조건 아래서 프로그래밍이 가능하다.

### 역할별 수행 작업

![Singleton](/assets/post/designpattern/Singleton.png)

* Singleton
  * Singleton 패턴에는 Singleton의 역할만 존재함
  * 유일한 인스턴스를 얻기 위한 static 메소드를 가지고 있고, 이 메소드는 언제난 동일한 인스턴스를 반환함

### 예제

```java
public class Singleton {
    private static Singleton singleton = new Singleton();
    private Singleton() {
        System.out.println("인스턴스를 생성했습니다.");
    }
    public static Singleton getInstance() {
        return singleton;
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println("Start.");
        Singleton obj1 = Singleton.getInstance();
        Singleton obj2 = Singleton.getInstance();
        if (obj1 == obj2) {
            System.out.println("obj1과 obj2는 같은 인스턴스입니다.");
        } else {
            System.out.println("obj1과 obj2는 같은 인스턴스가 아닙니다.");
        }
        System.out.println("End.");
    }
}
```

[GitHub](https://github.com/jsyang-dev/study-designpattern/tree/master/src/me/study/pattern/singleton/example) 소스 참고
