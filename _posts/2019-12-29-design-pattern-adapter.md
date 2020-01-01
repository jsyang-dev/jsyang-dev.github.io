---
title: 디자인 패턴 - Adapter
layout: post
subtitle: 바꿔서 재이용하기
tags:
- Java
- DesignPattern
- Study
author: Jeongsu Yang
comments: 'True'
---

## Adapter 패턴

### 정의

* 이미 제공되어 있는 것을 그대로 사용할 수 없을 때, 필요한 형태로 교환하고 사용하는 일이 자주 있다.
* '이미 제공되어 있는 것'과 '필요한 것' 사이의 '차이'를 없애주는 디자인 패턴이 Adapter 패턴이며, Wrapper 패턴으로 불리기도 한다.
* Adapter 패턴은 두 가지 종류가 있다.
  * 클래스에 의한 Adapter 패턴(상속을 사용한 Adapter 패턴)
  * 인스턴스에 의한 Adapter 패턴(위임을 사용한 Adapter 패턴)

### 사용 목적

* Adapter 패턴은 기존의 클래스를 개조해서 필요한 클래스를 만든다.

### 역할별 수행 작업

#### 클래스에 의한 Adapter 패턴

![Adapter1](/assets/post/designpattern/Adapter1.png)

#### 인스턴스에 의한 Adapter 패턴

![Adapter2](/assets/post/designpattern/Adapter2.png)

* Client
  * Target 역할의 메소드를 사용해서 일을 수행
* Target
  * 지금 필요한 메소드를 결정
* Adaptee
  * 이미 준비되어 있는 메소드를 가지고 있는 역할
* Adapter
  * Adaptee 역할의 메소드를 사용해서 어떻게든 Target 역할을 만족시키는 역할

### 예제

#### 클래스에 의한 Adapter 패턴

![AdapterExample1](/assets/post/designpattern/AdapterExample1.png)

```java
public interface Print {
    void printWeak();
    void printStrong();
}

public class PrintBanner extends Banner implements Print {
    public PrintBanner(String string) {
        super(string);
    }
    public void printWeak() {
        showWithParen();
    }
    public void printStrong() {
        showWithAster();
    }
}

public class Banner {
    private String string;
    public Banner(String string) {
        this.string = string;
    }
    public void showWithParen() {
        System.out.println("(" + string + ")");
    }
    public void showWithAster() {
        System.out.println("*" + string + "*");
    }
}

public class Main {
    public static void main(String[] args) {
        Print p = new PrintBanner("Hello");
        p.printWeak();
        p.printStrong();
    }
}
```

[GitHub](https://github.com/jsyang-dev/study-designpattern/tree/master/src/me/study/pattern/adapter/example1) 소스 참고

#### 인스턴스에 의한 Adapter 패턴

![AdapterExample2](/assets/post/designpattern/AdapterExample2.png)

```java
public abstract class Print {
    public abstract void printWeak();
    public abstract void printStrong();
}

public class PrintBanner extends Print {
    private Banner banner;
    public PrintBanner(String string) {
        this.banner = new Banner(string);
    }
    public void printWeak() {
        banner.showWithParen();
    }
    public void printStrong() {
        banner.showWithAster();
    }
}

public class Banner {
    private String string;
    public Banner(String string) {
        this.string = string;
    }
    public void showWithParen() {
        System.out.println("(" + string + ")");
    }
    public void showWithAster() {
        System.out.println("*" + string + "*");
    }
}

public class Main {
    public static void main(String[] args) {
        Print p = new PrintBanner("Hello");
        p.printWeak();
        p.printStrong();
    }
}
```

[GitHub](https://github.com/jsyang-dev/study-designpattern/tree/master/src/me/study/pattern/adapter/example2) 소스 참고
