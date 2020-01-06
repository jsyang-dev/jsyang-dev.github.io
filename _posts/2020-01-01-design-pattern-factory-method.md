---
title: 디자인 패턴 - Factory Method
layout: post
subtitle: 하위 클래스에서 인스턴스 작성하기
tags:
- Java
- DesignPattern
- Study
author: Jeongsu Yang
comments: 'True'
---

## Factory Method 패턴

### 정의

* Template Method 패턴을 인스턴스 생성에 적용한 것이 Factory Method 패턴이다.

### 사용 목적

* 인스턴스 생성을 위한 framework 패키지의 내용을 수정하지 않아도 전혀 다른 제품과 Factory를 만들 수 있다.

### 역할별 수행 작업

![FactoryMethod](/assets/post/designpattern/FactoryMethod.png)

* Product
  * 이 패턴에서 생성되는 인스턴스가 가져야 할 메소드를 결정하는 추상 클래스
* Creator
  * Product 역할을 생성하는 추상 클래스
* ConcreteProduct
  * 구체적인 Product를 결정
* ConcreteCreator
  * 구체적인 Product를 만드는 클래스를 결정

### 예제

![FactoryMethodExample](/assets/post/designpattern/FactoryMethodExample.png)

```java
public abstract class Factory {
    public final Product create(String owner) {
        Product p = createProduct(owner);
        registerProduct(p);
        return p;
    }
    protected abstract Product createProduct(String owner);
    protected abstract void registerProduct(Product product);
}

public abstract class Product {
    public abstract void use();
}

public class IDCardFactory extends Factory {
    private ArrayList<String> owners = new ArrayList<>();
    protected Product createProduct(String owner) {
        return new IDCard(owner);
    }
    protected void registerProduct(Product product) {
        owners.add(((IDCard)product).getOwner());
    }
    public ArrayList<String> getOwners() {
        return owners;
    }
}

public class IDCard extends Product {
    private String owner;
    IDCard(String owner) {
        System.out.println(owner + "의 카드를 만듭니다.");
        this.owner = owner;
    }
    public void use() {
        System.out.println(owner + "의 카드를 사용합니다.");
    }
    public String getOwner() {
        return owner;
    }
}
```

[GitHub](https://github.com/jsyang-dev/study-designpattern/tree/master/src/me/study/pattern/factorymethod/example) 소스 참고
