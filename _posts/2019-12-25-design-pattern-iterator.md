---
title: 디자인 패턴 - Iterator
layout: post
subtitle: 순서대로 지정해서 처리하기
tags:
- Java
- DesignPattern
- Study
author: Jeongsu Yang
comments: 'True'
---

## Iterator 패턴

### 정의

* 배열 arr의 모든 요소를 표시하기 위해서는 다음과 같이 for문을 사용한다.

```java
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}
```

* 이와 같이 i를 하나씩 증가시키면 배열 arr의 요소 전체를 처음부터 차례대로 검색하게 된다.
* 여기에서 사용되고 있는 변수 i의 기능을 추상화해서 일반화한 것을 디자인 패턴에서는 Iterator 패턴이라고 한다.
* 즉, Iterater 패턴은 무엇인가 많이 모여있는 것들을 순서대로 지정하면서 전체를 검색하는 처리를 실행하기 위한 것이다.

### 사용 목적

* Iterator를 사용함으로써 구현과 분리해서 하나씩 세는 것이 가능하다.

### 역할별 수행 작업

![Iterator](/assets/post/designpattern/Iterator.png)

* Iterator
  * 요소를 순서대로 검색해가는 메소드를 결정
* ConcreteIterator
  * Iterator 역할이 결정한 메소드를 실제로 구현함
  * 검색하기 위해 필요한 정보를 가지고 있어야 함
* Aggregate
  * Iterator를 만들어내는 메소드를 결정함
* ConcreteAggregate
  * Aggregate 역할이 결정한 메소드를 실제로 구현하는 일을 함
  * ConcreteIterator 역할의 인스턴스를 만듦

### 예제

![IteratorExample](/assets/post/designpattern/IteratorExample.png)

```java
public interface Aggregate {
    Iterator iterator();
}

public class BookShelf implements Aggregate {
    private Book[] books;
    private int last = 0;
    public BookShelf(int maxsize) {
        this.books = new Book[maxsize];
    }
    public Book getBookAt(int index) {
        return books[index];
    }
    public void appendBook(Book book) {
        this.books[last] = book;
        last++;
    }
    public int getLength() {
        return last;
    }
    public Iterator iterator() {
        return new BookShelfIterator(this);
    }
}

public interface Iterator {
    boolean hasNext();
    Object next();
}

public class BookShelfIterator implements Iterator {
    private BookShelf bookShelf;
    private int index;
    public BookShelfIterator(BookShelf bookShelf) {
        this.bookShelf = bookShelf;
        this.index = 0;
    }
    public boolean hasNext() {
        if (index < bookShelf.getLength()) {
            return true;
        } else {
            return false;
        }
    }
    public Object next() {
        Book book = bookShelf.getBookAt(index);
        index++;
        return book;
    }
}

public class Book {
    private String name = "";
    public Book(String name) {
        this.name = name;
    }
    public String getName() {
        return name;
    }
}

public class Main {
    public static void main(String[] args) {
        BookShelf bookShelf = new BookShelf(4);
        bookShelf.appendBook(new Book("Around the World in 80 Days"));
        bookShelf.appendBook(new Book("Bible"));
        bookShelf.appendBook(new Book("Cinderella"));
        bookShelf.appendBook(new Book("Daddy-Long-Legs"));
        Iterator it = bookShelf.iterator();
        while (it.hasNext()) {
            Book book = (Book)it.next();
            System.out.println("" + book.getName());
        }
    }
}
```

[GitHub](https://github.com/jsyang-dev/study-designpattern/tree/master/src/me/study/pattern/iterator/example) 소스 참고
