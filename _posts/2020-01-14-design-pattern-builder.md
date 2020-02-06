---
title: 디자인 패턴 - Builder
layout: post
subtitle: 복잡한 인스턴스 조립하기
tags:
- java
- designpattern
author: Jeongsu Yang
comments: 'True'
---

## Builder 패턴

### 정의

* 전체를 구성하고 있는 각 부분을 만들고 단계를 밟아 만들어가는 패턴이다.

### 사용 목적

* 구체적인 하위 클래스를 모르기 때문에 교환이 가능하다.

### 역할별 수행 작업

![Builder](/assets/post/designpattern/Builder.png)

![BuilderSequence](/assets/post/designpattern/BuilderSequence.png)

* Builder
  * 인스턴스를 생성하기 위한 메소드를 결정함
* ConcreteBuilder
  * Builder 역할의 메소드를 구현하고 있는 클래스
  * 실제의 인스턴스 작성으로 호출되는 메소드가 여기에 정의됨
* Diretor
  * Builder 역할의 메소드를 사용해서 인스턴스를 생성함
* Client
  * Builder 패턴을 이용하는 역할

### 예제

![BuilderExample](/assets/post/designpattern/BuilderExample.png)

```java
public class Director {
    private Builder builder;
    public Director(Builder builder) {
        this.builder = builder;
    }
    public Object construct() {
        builder.makeTitle("Greeting");
        builder.makeString("아침과 낮에");
        builder.makeItems(new String[]{
            "좋은 아침입니다.",
            "안녕하세요",
        });
        builder.makeString("밤에");
        builder.makeItems(new String[]{
            "안녕하세요",
            "안녕히 주무세요",
            "안녕히 계세요",
        });
        return builder.getResult();
    }
}

public abstract class Builder {
    public abstract void makeTitle(String title);
    public abstract void makeString(String str);
    public abstract void makeItems(String[] items);
    public abstract Object getResult();
}

public class TextBuilder extends Builder {
    private StringBuffer buffer = new StringBuffer();
    public void makeTitle(String title) {
        buffer.append("==============================\n");
        buffer.append("『" + title + "』\n");
        buffer.append("\n");
    }
    public void makeString(String str) {
        buffer.append("■" + str + "\n");
        buffer.append("\n");
    }
    public void makeItems(String[] items) {
        for (int i = 0; i < items.length; i++) {
            buffer.append("●" + items[i] + "\n");
        }
        buffer.append("\n");
    }
    public Object getResult() {
        buffer.append("==============================\n");
        return buffer.toString();
    }
}

public class HTMLBuilder extends Builder {
    private String filename;
    private PrintWriter writer;
    public void makeTitle(String title) {
        filename = title + ".html";
        try {
            writer = new PrintWriter(new FileWriter(filename));
        } catch (IOException e) {
            e.printStackTrace();
        }
        writer.println("<html><head><title>" + title + "</title></head><body>");
        writer.println("<h1>" + title + "</h1>");
    }
    public void makeString(String str) {
        writer.println("<p>" + str + "</p>");
    }
    public void makeItems(String[] items) {
        writer.println("<ul>");
        for (int i = 0; i < items.length; i++) {
            writer.println("<li>" + items[i] + "</li>");
        }
        writer.println("</ul>");
    }
    public Object getResult() {
        writer.println("</body></html>");
        writer.close();
        return filename;
    }
}

public class Main {
    public static void main(String[] args) {
        if (args.length != 1) {
            usage();
            System.exit(0);
        }
        if (args[0].equals("plain")) {
            Director director = new Director(new TextBuilder());
            String result = (String)director.construct();
            System.out.println(result);
        } else if (args[0].equals("html")) {
            Director director = new Director(new HTMLBuilder());
            String filename = (String)director.construct();
            System.out.println(filename + "이 작성되었습니다.");
        } else {
            usage();
            System.exit(0);
        }
    }
    public static void usage() {
        System.out.println("Usage: java Main plain      일반 텍스트에서 문서작성");
        System.out.println("Usage: java Main html       HTML 파일에서 문서작성");
    }
}
```

[GitHub](https://github.com/jsyang-dev/study-designpattern/tree/master/src/me/study/pattern/builder/example) 소스 참고
