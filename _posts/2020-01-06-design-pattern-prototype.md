---
title: 디자인 패턴 - Prototype
layout: post
subtitle: 복사해서 인스턴스 만들기
tags:
- Java
- DesignPattern
- Study
author: Jeongsu Yang
comments: 'True'
---

## Factory Method 패턴

### 정의

* 클래스 이름을 지정하지 않고 인스턴스를 생성하는 패턴이다.

### 사용 목적

* 다음과 같이 클래스로부터 인스턴스를 만드는 것이 어려운 경우에 사용한다.
  * 종류가 너무 많아 클래스로 정리되지 않는 경우
  * 클래스로부터 인스턴스 생성이 어려운 경우
  * framework와 생성할 인스턴스를 분리하고 싶은 경우

### 역할별 수행 작업

![Prototype](/assets/post/designpattern/Prototype.png)

* Prototype
  * 인스턴스를 복사하여 새로운 인스턴스를 만들기 위한 메소드를 결정함
* ConcretePrototype
  * 인스턴스를 복사해서 새로운 인스턴스를 만드는 메소드를 실제로 구현함
* Client
  * 인스턴스를 복사하는 메소드를 이용해서 새로운 인스턴스를 만듦

### 예제

![PrototypeExample](/assets/post/designpattern/PrototypeExample.png)

```java
public class Manager {
    private Hashtable showcase = new Hashtable();
    public void register(String name, Product proto) {
        showcase.put(name, proto);
    }
    public Product create(String protoname) {
        Product p = (Product)showcase.get(protoname);
        return p.createClone();
    }
}

public interface Product extends Cloneable {
    void use(String s);
    Product createClone();
}

public class UnderlinePen implements Product {
    private char ulchar;
    public UnderlinePen(char ulchar) {
        this.ulchar = ulchar;
    }
    public void use(String s) {
        int length = s.getBytes().length;
        System.out.println("\""  + s + "\"");
        System.out.print(" ");
        for (int i = 0; i < length; i++) {
            System.out.print(ulchar);
        }
        System.out.println(" ");
    }
    public Product createClone() {
        Product p = null;
        try {
            p = (Product)clone();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        return p;
    }
}

public class MessageBox implements Product {
    private char decochar;
    public MessageBox(char decochar) {
        this.decochar = decochar;
    }
    public void use(String s) {
        int length = s.getBytes().length;
        for (int i = 0; i < length + 4; i++) {
            System.out.print(decochar);
        }
        System.out.println("");
        System.out.println(decochar + " "  + s + " " + decochar);
        for (int i = 0; i < length + 4; i++) {
            System.out.print(decochar);
        }
        System.out.println("");
    }
    public Product createClone() {
        Product p = null;
        try {
            p = (Product)clone();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        return p;
    }
}

public class Main {
    public static void main(String[] args) {
        // 준비
        Manager manager = new Manager();
        UnderlinePen upen = new UnderlinePen('~');
        MessageBox mbox = new MessageBox('*');
        MessageBox sbox = new MessageBox('/');
        manager.register("strong message", upen);
        manager.register("warning box", mbox);
        manager.register("slash box", sbox);

        // 생성
        Product p1 = manager.create("strong message");
        p1.use("Hello, world.");
        Product p2 = manager.create("warning box");
        p2.use("Hello, world.");
        Product p3 = manager.create("slash box");
        p3.use("Hello, world.");
    }
}
```

[GitHub](https://github.com/jsyang-dev/study-designpattern/tree/master/src/me/study/pattern/prototype/example) 소스 참고
