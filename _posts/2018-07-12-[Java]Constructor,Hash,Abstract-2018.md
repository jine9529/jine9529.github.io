---
layout:     post

title:      "[Java]Constructor,Hash,Abstract"

subtitle:   " \"Java Class Day08 2018\""

date:       2018-07-12 09:00:00

author:     "Jine"

header-img: "img/post-bg-2015.jpg"

catalog: true

tags:
    - MultiCampus

---

### 생성자

constructor

객체가 생성될때 호출되는 메서드

#### 특징

- 반환유형 자체가 없음. void가 아니고 반환유형이라는 문법자체가 없음
- 함수명이 클래스 이름과 같음
- 접근지정자가 일반적으로 public
- 메소드이기때문에 오버로딩이 가능하다. (생성자 여러개 가능)



- new 연산자가 객체를 만들기 위해서 생성자를 호출한다.

  C++에서는 Car oppaCha = Car(); 하면 스택영역에 만들고 new를 붙이면 힙 영역에 생성된다.

- 생성자를 하나도 정의하지 않으면 자동으로 몸통이 비어있는(매개변수없는) 생성자가 하나 만들어진다.  이를 **디폴트 생성자**라고 부른다.
- 일반적으로 필드들의 초기값을 설정





```java
public int sum(int ...numbers) { //가변길이 인자를 받는방법, numbers는 배열임
			System.out.println(numbers.length);
			System.out.println(numbers[0]);
			int sum = 0;
			for(int n : numbers)
				sum += n;
			return sum;
	}
```



**궁금한 함수있으면 F3 누르기!**



#### Hash

- 충돌이 잘 일어나지 않는다.

- 입력은 많아도 출력은 정해져 있다. (커다란게 들어가도 작은게 나온다.)

  ex) 로그인 처리, 나의 아이디 비밀번호를 hash함수에 넣으면 맞다 틀리다만 알 수 있음

  ex) 파일다운로드할때 (SHA-512, 파일을 다운받았을때 나오는 문자열이 일치하면 다운로드를 제대로 받았음을 확인할 수 있다.)

  ex) 비트코인, 블록체인



## ROBOT 예제

> 여러가지 개념들을 배우기 전에 Robot을 하나 만들어본다.

```java
//로봇을 참조하는 펀치공격과 날아서이동하는 태권로봇을 만들자.
package Robot;

public class Taekwon extends Robot{
    public void attack(){
        system.out.println("펀치공격!");
    }
    public void move(){
        system.out.println("날아서 이동!");
    }
}
```

```java
//로봇을 참조하는 미사일공격과 걸어서이동하는 마징가로봇을 만들자.
package Robot;

public class Mazinga extends Robot{
    public void attack(){
        system.out.println("미사일 공격!");
    }
    public void move(){
        system.out.println("걸어서 이동!")
    }
}
```

```java
//공격, 이동기능이 있음을 추상클래스로 표시
//공격기능은 이동 -> 공격 -> 이동 을 동작하게함.
package Robot;

public abstract class Robot{
    public abstract void attack();
    public abstract void move();
    public void fight(){
        move();
        attack();
        move();
    }
}
```

```java
//이를 토대로 작동을 시켜보자.
package Robot;

public class RobotTest{
    public static void main(String[] args){
        Robot t = new Taekwon();
        Robot m = new Mazinga();
        
        t.fight();
        m.fight();
    }
}
```

![image](https://user-images.githubusercontent.com/33712866/42668470-c94e4a2e-868b-11e8-8ae5-28ac87cb281d.png)

##### 템플릿 메소드 패턴을 적용!

상위 클래스에서 처리의 흐름을 제어하며 (여기 예제에서는 fight ),

하위클래스에서 처리의 내용을 구체화한다. (attack, move)

ex) 웹사이트는 전부 요청 -> 응답 하는 구조로 얼추 비슷하다.

그러면 우리는 요청하면 응답하는 '템플릿'을 만들어 놓고 상속바당서  '어떻게' 만 계속 구현해나가면 된다.

> Robot (이것이 템플릿메소드 패턴)

```java
public class Robot{
    puvlic void attack(){
        system.out.println("아몰랑자식이 구현하겠지");
    }
    public void fight(){
        attak();
    }
}
```

부모클래스에서 전체 흐름을 규정한다.

fight 안의  attack()과 같은 실제 내부 동작은 자식들이 구현한다.

```java
public class Taekwon extends Robot{
    public void attack(){
        system.out.println("펀치로 공격!");
    }
}
```





## 추상클래스 abstract

추상클래스 (abstract class)

몸체가 구현되지 않은 메소드를 가지고 있는 클래스

몸통이 없고 abstract 키워드가 붙는다.

> 추상클래스 적용한 Robot

```java
public abstract class Robot{
    public abstract void attack();
    public void fight(){
        attak();
    }
}
```

추상메소드를 가지려면 클래스도 추상클래스여야한다.

추상클래스는 미완성 설계도이기 때문에 객체를 만들수 없다.

RobotTest 에서 Robot r= new Robot(); //불가

그래도 사용하고 싶다면 미완성 부분에 대해 1회성 구현하는 **익명클래스**사용

```java
Robot r = new Robot(){
    public void attack(){
    }
}
```



#### 단일 책임 원칙 (S) 중요!!

> PunchAttack, MissileAttack, WalikingMove, FlyingMove 생성

```java
public class PunchAttack{
    public void attack(){
        system.out.println("펀치로 공격!");
    }
}
```

세개 더...이런식으로 작성....(생략)

>Robot 

```java
public abstract class Robot{
    public abstract void attack();
    public abstract void move();
    public void fight(){
        move();
        attack();
    }
}
```



> Robot을 상속받은 Taekwon

```java
public class Taekwon extends Robot{
    private PunchAttack attack;
    private FlyingMove move;
    public Taekwon(){
        attack = new PunchAttack();
        move = new FlyingMove();
    }
    @Override
    public void attack(){
        attack.attack();
    }
    @Override
    public void move(){
        move.move();
    }
}
```

단일 책임 원칙을 적용했더니, 여러개의 로봇이 펀치공격기능을 사용하더라도 펀치공격기능은 여러번 구현될 필요가 없이 펀치공격 클래스를 '사용'하기만 하면 된다.

-> 참조변수를 준비하고 객체를 생성해야 한다.



그러나 아직  타입에 의존적이고,

    private PunchAttack attack;
    private FlyingMove move;
객체 생성에 의존성을 가지고 있다.

    public Taekwon(){
        attack = new PunchAttack();
        move = new FlyingMove();
    }
우리가 보기에는 이렇지만, 컴퓨터는 각각의 클래스로 인식한다.

PunchAttack & MissileAttack -> 공격

FlyingMove & WalkingMove -> 이동

공격에서는 둘다 attack이란 메서드가 있으니, attack 추상 메소드를 갖는 클래스를 만들어서 부모로 잡아주면 둘이는 형제가 된다.



### 위 ROBOT을 각 공격과 이동들이 부모를 모시도록!

> Attack 규격

```java
public abstract class Attack{
    public abstract void attack();
}
```

멤버변수도 없고 구현된 메소드도 없다.

단지 추상메소드 하나 가지고 있으니 규격같은 느낌!

이 아이를 상속받은 클래스의 객체는 공격할 수 있다!!!

> Attack을 상속받은 PunchAttack (MisilleAttack도 똑같이! 여기선 생략)

```java
public class PunchAttack extends Attack{
    public void attack(){
        system.out.println("펀치로 공격!");
    }
}
```



> Robot을 상속받은 Mazinga ( Teakwon도 똑같이! 여기선 생략)

```java
public class Mazinga extends Robot{
    private Attack attack;
    private WalkingMove move;
    public Mazinga(){
        attack = new MissileAttack();
        move = new WalkingMove();
    }
}
```



>RobotTest

```java
public class RobotTest{
    public static void main(String[] args){
        Robot t = new Taekwon();
        Robot m = new Mazinga();
        
        t.fight();
        m.fight();
    }
}
```

