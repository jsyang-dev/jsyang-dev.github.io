---
title: 디자인 패턴 02
layout: post
subtitle: 어댑터 패턴
tags:
- Java
- DesignPattern
- Study
author: Jeongsu Yang
comments: 'True'
---

## 어댑터 패턴

### 정의

* 행위를 클래스로 캡슐화해 동적으로 행위를 자유롭게 바꿀 수 있게 해주는 패턴
* 즉, 전략을 쉽게 바꿀 수 있도록 해주는 디자인 패턴이다.

### 역할별 수행 작업

![Adapter](/assets/designpattern/post/Adapter.png)

* Adapter
* ConcreteAdapter
* Adaptee

### 예제

![AdapterExample](/assets/designpattern/post/AdapterExample.png)

```java
public interface SocketAdapter {
    public Voltage get120Volt();
    public Voltage get200Volt();
    public Voltage get220Volt();
}

public class SocketAdapterImpl implements SocketAdapter {
    private Socket socket = new Socket();

    @Override
    public Voltage get120Volt() {
        Voltage voltage = socket.getVoltage();
        return convertVoltage(voltage, 100);
    }

    @Override
    public Voltage get200Volt() {
        Voltage voltage = socket.getVoltage();
        return convertVoltage(voltage, 20);
    }

    @Override
    public Voltage get220Volt() {
        return socket.getVoltage();
    }

    private Voltage convertVoltage(Voltage voltage, int convertValue) {
        return new Voltage(voltage.getValue() - convertValue);
    }
}

public class Voltage {
    private int value;

    public Voltage(int value) {
        this.value = value;
    }

    public int getValue() {
        return value;
    }

    public void setValue(int value) {
        this.value = value;
    }
}
```

[GitHub](https://github.com/jsyang-dev/study-designpattern.git) 소스 참고
