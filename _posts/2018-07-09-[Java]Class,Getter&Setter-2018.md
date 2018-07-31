---
layout:     post
title:      "[JAVA]Class&Method, Getter&Setter"
subtitle:   " \"Java Class Day05 2018\""
date:       2018-07-09 09:00:00
author:     "Jine"
header-img: "img/post-bg-js-module.jpg"
tags:
    - MultiCampus
---

## 클래스와 메소드

> ##### 절차지향 vs 객체지향

- 절차지향

  구조체와 함수가 별도로 존재

- 객체지향

  관련있는 변수와 함수가 하나로 묶임



변수로 받을수 있는 것을 **매개변수**라 한다.

매개변수로 전달되어지는 값을 **파라메터**라고 부른다.



> ##### class 란

관련있는 변수와 함수를 묶어놓은 사용자정의 자료형



> class Car 예제

```java
public class Car {
	
	public int speed;
	public void speedUp() {
		speed += 10;	
	}
	public String toString() {
		return "속도: " + speed;
	}
}
```
```java
public class CarTest {
	public static void main(String[] args) {
		Car myCar = new Car(); //첫번째 객체 생성
		myCar.speed = 60; //객체의 필드 변경
		myCar.speedUp(); //객체의 메소드 호출
		System.out.println(myCar);
    }
}
```

```
출력결과
속도:  70
```

객체를 println하면 객체.toString이라고 생각하기 (이후에 배움)

그 전에 toString을 꼭 정의해줘야함



> ##### 객체의 소멸

JVM안에는 가비지컬렉터라고 하는 청소부가 주기적으로 돌아다니면서 소멸조건을 만족시키는 객체를 죽이고 다님



> ##### 메소드 오버로딩

##### 중복메소드

메소드 오버로딩

반환값과 이름이 같은데 매개변수가 다른 여러개의 메소드를 정의하는 것



## 설정자와 접근자 (Setter & Getter)

private 수식어가 붙은 상태나 동작(필드나 메서드)는 내부에서는 접근이 가능하지만, 클래스 외부에서는 접근이 불가



> ##### 접근권한을 왜 만들었을까?

관련있는 상태와 기능을 하나로 묶자는게 객체지향의 출발이고 이것이 클래스이다.<br>잘 설계된 클래스는 public 인터페이스만을 통하여 클라이언트가 원하는 기능을 제공하고 디테일한 구현은 감춤으로써 코드를 유연하게 만들 수 있다.<br>코드상에서 잠재적인 버그를 만들 수 있는 확률을 확실하게 줄여주며, 컴파일시에 잡을 수 있게 도와준다. 



> ##### 캡슐화, 은닉화

일반적으로 상태는 객체 내부에서만 조작 가능하도록 private으로 감춘다.



> ##### 사용하면 좋은점

- 상태값을 은닉화시켜서 객체지향원칙에 더 충실, **입력값에 대한 검정**을 할 수 있다.
- 기록을 한다던가 log를 찍을 수 있다.
- getter/setter 중 하나만 제공하면 읽기전용 혹은 쓰기전용 **접근권한 세분화**

> ##### 단축키

alt + shift + s -> r

source -> generate getter and setter

> 객체를 출력하고 싶다면..?

Employee.java (class)

```java
public String toString() {
		return "이름: "+ getName();
	}
```

EmployeeTest.java (main)

```java
System.out.println(A);
```

toString( )설정 안해주면 주소값이 출력된다.