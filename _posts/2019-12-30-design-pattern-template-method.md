---
title: 디자인 패턴 - Template Method
layout: post
subtitle: 하위 클래스에서 구체적으로 처리하기
tags:
- Java
- DesignPattern
- Study
author: Jeongsu Yang
comments: 'True'
---

## Template Method 패턴

### 정의

* 상위 클래스에서 처리의 뼈대를 결정하고, 하위 클래스에서 그 구체적인 내용을 결정하는 디자인 패턴이 Template Method 패턴이다.

### 사용 목적

* 상위 클래스의 템플릿 메소드에 알고리즘이 기술되어 있으므로, 하위 클래스에서는 알고리즘을 일일이 기술할 필요가 없다.

### 역할별 수행 작업

![TemplateMethod](/assets/post/designpattern/TemplateMethod.png)

* AbstractClass
  * 템플릿 메소드를 구현함
  * 템플릿 메소드에서 사용하고 있는 추상 메소드를 선언함
* ConcreteClass
  * AbstractClass 역할에서 정의 되어 있는 추상 메소드를 구체적으로 구현함

### 예제

![TemplateMethodExample](/assets/post/designpattern/TemplateMethodExample.png)

```java
public abstract class AbstractDisplay {
    public abstract void open();
    public abstract void print();
    public abstract void close();
    public final void display() {
        open();
        for (int i = 0; i < 5; i++) {
            print();
        }
        close();
    }
}

public class CharDisplay extends AbstractDisplay {
    private char ch;
    public CharDisplay(char ch) {
        this.ch = ch;
    }
    public void open() {
        System.out.print("<<");
    }
    public void print() {
        System.out.print(ch);
    }
    public void close() {
        System.out.println(">>");
    }
}

public class StringDisplay extends AbstractDisplay {
    private String string;
    private int width;
    public StringDisplay(String string) {
        this.string = string;
        this.width = string.getBytes().length;
    }
    public void open() {
        printLine();
    }
    public void print() {
        System.out.println("|" + string + "|");
    }
    public void close() {
        printLine();
    }
    private void printLine() {
        System.out.print("+");
        for (int i = 0; i < width; i++) {
            System.out.print("-");
        }
        System.out.println("+");
    }
}

public class Main {
    public static void main(String[] args) {
        AbstractDisplay d1 = new CharDisplay('H');
        AbstractDisplay d2 = new StringDisplay("Hello, world.");
        AbstractDisplay d3 = new StringDisplay("Design Pattern");
        d1.display();
        d2.display();
        d3.display();
    }
}
```

[GitHub](https://github.com/jsyang-dev/study-designpattern/tree/master/src/me/study/pattern/templatemethod/example1) 소스 참고
