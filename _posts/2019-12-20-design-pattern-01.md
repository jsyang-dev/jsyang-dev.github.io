---
title: 디자인 패턴 01
layout: post
subtitle: 스트래티지 패턴
tags:
- Java
- DesignPattern
- Study
author: Jeongsu Yang
comments: 'True'
---

## 스트레티지 패턴

### 정의

* 행위를 클래스로 캡슐화해 동적으로 행위를 자유롭게 바꿀 수 있게 해주는 패턴
* 즉, 전략을 쉽게 바꿀 수 있도록 해주는 디자인 패턴이다.

### 역할별 수행 작업

![Strategy](/assets/post/designpattern/Strategy.png)

* Strategy
  * 인터페이스나 추상 클래스로 외부에서 동일한 방식으로 알고리즘을 호출하는 방법을 명시
* ConcreteStrategy
  * 스트래티지 패턴에서 명시한 알고리즘을 실제로 구현한 클래스
* Context
  * 스트래티지 패턴을 이용하는 역할을 수행한다.
  * 필요에 따라 동적으로 구체적인 전략을 바꿀 수 있도록 setter 메서드(‘집약 관계’)를 제공한다.

### 예제

![StrategyExample](/assets/post/designpattern/StrategyExample.png)

```java
public class Character {
    private Weapon weapon;

    public void setWeapon(Weapon weapon) {
        this.weapon = weapon;
    }

    public void attack() {
        this.weapon.doAttack();
    }
}

public interface Weapon {
    void doAttack();
}

public class Sword implements Weapon {
    @Override
    public void doAttack() {
        System.out.println("검 공격");
    }
}

public class Bow implements Weapon {
    @Override
    public void doAttack() {
        System.out.println("활 공격");
    }
}

public class Ax implements Weapon {
    @Override
    public void doAttack() {
        System.out.println("도끼 공격");
    }
}
```
