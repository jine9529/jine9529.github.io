---
layout:     post

title:      "[Java] SOLID,Exception"

subtitle:   " \"Java Class Day09 2018\""

date:       2018-07-13 09:00:00

author:     "Jine"

header-img: "img/post-bg-2015.jpg"

catalog: true

tags:
    - MultiCampus


---











## 객체지향의 큰 틀

#### 기본개념

-절치지향

함수

-객체지향

변수+함수 -> 정리 ->클래스

수직, 공통 -> 상속

수평, 공통 -> 다형성

=>디자인패턴 ->프레임워크



##### spring framework가 많이 쓰이는 이유

우리나라는 모든 사업이 정부주도적으로 돌아가고, 공정하게 하기위해 공모로 입찰을 하게됨

공정해야 하기 때문에 2년에 한번씩 다시 입찰해야함

각자 기업별로 프레임워크가 있지만 상호호환이 안됨.

정부가 기업 모아놓고 강제로 만들었음 ->전자정보 프레임워크가 만들어짐(2009)

이게 spring 프레임워크를 기반으로 만들어짐



-----

## solid 원칙

![image](https://user-images.githubusercontent.com/33712866/42673163-f0dca7a2-86a4-11e8-9faa-fe9386bd2ded.png)

[위키피디아](https://ko.wikipedia.org/wiki/SOLID_(%EA%B0%9D%EC%B2%B4_%EC%A7%80%ED%96%A5_%EC%84%A4%EA%B3%84))

인터페이스 분리 원칙(I)와 의존관계 역전 원칙(D)를 하나씩 로봇예제에 적용해볼 것이다.

-----



## ROBOT

인터페이스

추상메소들의 집합

extends 대신에 implements 키워드를 사용

어차피 추상케소드만 있으니까 abstract 키워드는 생략이 가능



#### 인터페이스 분리원칙

자신이 이용하지 않는 메서드에 의존하지 않아야 한다는 원칙

> 인터페이스 Move, Attack 생성

```java
//인터페이스로 이동을 만든다.
public interface Move{
    public void move();
}
```

```java
//인터페이스로 공격을 만든다.
public interface Attack{
    public void attack();
}
```

> implements 펀치, 미사일, 걸어서, 날아서 구현

```java
//인터페이스 Attack을 implements 받음
public class PunchAttack implements Attack{
    @Override
    public void attack(){
        system.out.println("펀치로 공격!");
    }
 }
```

```java
public class MissileAttack implements Attack{
    @Override
    public void attack(){
        ststem.out.println("미사일로 공격!");
    }
}
```

```java
public class FlyingMove implements Move{
    @Override
    public void move(){
        system.out.println("날아서 이동!");
    }
}
```

```java
public class WalkingMove implements Move{
    @Override
    public void move(){
        system.out.println("걸어서 이동!");
    }
}
```

> 로봇의 추상클래스 작성 (뒷부분에 대폭 수정)

```java
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

> 태권 만들기 (의존버전)

```java
public class Taekwon extends Robot{
    private PunchAttack attack = new PunchAttack();
    //Taekwon은 PunchAttack이라는 구체화된 아이에게 의존했음
    //타입을 지정해서 의존 & 객체만들면서 의존
    //->이거보다는 좀 더 추상화되어있는 Attack 인터페이스에 의존하는게 더 낫다.
    @Override
    public void attack(){
        //내가 attack메소드를 수현할 건 아니고,
        //PunchAttack에 구현돼있는 기능을 사용할것임
        attack.attack();	//느슨한 결합
    }
    @Override
    public void move(){
        
    }
}
```

private Attack attack = new PunchAttack();

PunchAttack을 Attack으로 바꾼다고 해도 new 뒤의 PunchAttack();이 있다.

이말은 어차피 내가 PunchAttack객체를 만들어야 하므로 의미가 없다는 것이다.



하지만 내가 attack()을 만들필요없이 setter을 통해서 누군가가 대신 만들어서 나를 준다고 생각해보자



내가 사용해야될 객체를 내가 만드는게 아니라(내가 의존)

다른 누군가가 대신 만들어서 나한테 주는 것이다.

이를 **의존성 주입, 의존관계 역전**이라 한다.



#### 의존관계 역전

> 태권 만들기(의존x 버전)

```java
public class Taekwon extends Robot{
    private Arrack attack;
    public void setAttack(Attact attack){
        this.attack = attack;
    }
    
    @Override
    public void attack(){
        attack.attack();	
    }
    @Override
    public void move(){
    }
}
```

```java
 private PunchAttack attack = new PunchAttack(); //를
```

 ```java
private PunchAttack attack = new PunchAttack(); 

  private Arrack attack;
  public void setAttack(Attact attack){
        this.attack = attack; } //이렇게 바꾸면
 ```

누군가는 펀치어택을만들어서 내 setAttack에 넣어줘야겠지만

(그놈은 펀치어택에 의존하겠지만)나는 의존하지 않는다.



> 마징가 만들기 (태권도 의존 x와 같은 방식으로)

```java
public class Mazinga extends Robot{
    private Attack attack;
    public void setAttack(Attack attack){
        this.attack = attack;
    }
    @Override
    public void attack(){
        attack.attack();	
    }
    @Override
    public void move(){
    }
}
```

마징가를 만들었는데, 태권이랑 마징가랑 차이가 없어졌다!

```java
    private PunchAttack attack = new PunchAttack();
```

이런식으로 구체화된 펀치어택에 의존했다면, 두개의 코드가 달라졌을 것이다. 

```java
this.attack = attack; 
```

타인이 느슨해진다.

객체생성 의존성은 없앨 수 없고, 역전만 가능하다.

    private Attack attack;
    public void setAttack(Attack attack){
        this.attack = attack;
모든 자식이 공통된 코드이므로 부모로 묶어보자

```java
@Override
    public void attack(){
        attack.attack();
    }
```

attack() 도 이제 서로 같으므로 추상메소드일 필요없이 부모가 구현하도록 해보자

> Robot (수정한 코드)

```java
public abstract class Robot{
    private Attack attack;
    private Move move;
    public void setAttack(Attack attack){
        this.attack = attack;
    }
    public void setMove(Move move){
        this.move = move;
    }
    public void attack(){
        attack.attack();
    }
    public void move(){
        move.move();
    }
    public void fight(){
        move();
        attack();
        move();
    }
}
```



> RobotTest

```java
public class RobotTest {
	public static void main(String[] args) {
		PunchAttack pa = new PunchAttack();
		MissileAttack ma = new MissileAttack();
		WalkingMove wm = new WalkingMove();
		FlyingMove fm = new FlyingMove();
		
		Robot taekwon = new Robot();
		taekwon.setAttack(pa);
		taekwon.setMove(fm);
		Robot mazinga = new Robot();
		mazinga.setAttack(ma);
		mazinga.setMove(wm);
		Robot humanoid = new Robot();
		humanoid.setAttack(ma);
		humanoid.setMove(fm);
		
		taekwon.fight();	
	}
}
```

![image](https://user-images.githubusercontent.com/33712866/42673114-c3f2e2b0-86a4-11e8-9099-53b129859cee.png)



-----



## 내부클래스 생성자

내부클래스

클래스 안의 클래스

```java
package ex02;

public class OuterClass {
	private String secret = "Time is money";
	
	public OuterClass() {
		InnerClass obj = new InnerClass();
        //객체안에서 new
		obj.method();
	}
	
	private class InnerClass{
       //public static class InnerClass{}라면
		public InnerClass() {
			System.out.println("내부 클래스 생성자입니다.");
		}
		public void method() {
			System.out.println(secret);
		}
	}
    public static void main(String args[]) {
		OuterClass oc = new OuterClass();
		InnerClass ic = oc.new InnerClass();
       //OuterClass.InnerClass ic = new OuterClass.InnerClass();
	}
}
```

전부다 OuterClass의 멤버 ( secret, OuterCalss(), InnerClass() )



내부클래스에서 외부클래스의 멤버들을 쉽게 접근할 수있음

외부클래스 내부에서만 사용되는 클래스에 대해 캡슐화



-----



## 무명클래스

추상클래스나 인터페이스(추상메소드를 가진애들)은 객체화 될 수 없는데,

객체화와 동시에 미완성 부분을 일회성으로 완성시켜주는 방법



-----



## 예외처리

예외 : runtime Exception....

프로그램 실행 도중 문제가 생겨서 문제를 처리하지 않으면 프로그램이 종료된다.

##### 프로그램 오류

- 컴파일 에러
- 런타임 에러
- 논리적 에러



#### 예외 종류

![image](https://user-images.githubusercontent.com/33712866/42675057-3da0956e-86ad-11e8-82d3-d647e9547ee0.png)*

출처 : 인피니티 북스



크게 RuntimeException / IOException / Error 세가지로 나눈다.

- RuntimeException

  **언체킹익셉션**

  선택적 예외처리 대상

  - ArrayIndexOutOfBoundException

    배열의 잘못된 인덱스에 참조하면 프로그램이 종료된다.

    if ( i < arr.length )

  - ClassCastException

    객체를 형변환할때 잘못된 타입으로하면 프로그램이 종료

    if  ( obj instanceof anything )

  - NullPointerException

    참조값이 없는 참조변수에 . 연산자를 통해 접근하면 프로그램이 종료

    if ( obj != null )

- IOException

  **체킹익셉션**

  필수적 예외처리대상

  IO -> 밖에서 무언가 입력되거나 밖으로 뭔가 출력하는것

  혼자만의 문제가 아니기 때문에 꼭 예외처리를 해줘야되고 컴파일러가 검사한다.

- Error

  예외처리대상이 아님 (권한 밖)

  

  

  #### try-catch



```java
public class DivideByZeroOK {
	public static void main(String[] args) {
		int x = 1;
		int y = 0;
		try {
			System.out.println("아직 에러나기 전이지롱");
			int result = x / y;
			System.out.println(result);
		}  // 이 안에서는 ArithmeticException에 대해서만 안전하다.
		catch(ArithmeticException e) {
			System.out.println("0으로 나눌 수 없습니다.");
		}
		System.out.println("프로그램은 계속 진행됩니다.");
	}
}
```

![image](https://user-images.githubusercontent.com/33712866/42673823-2481a7c6-86a8-11e8-85de-05dab92bd005.png)

**여러종류의 에러**를 잡고싶으면 **catch 여러개**를넣으면 된다.

에러는 두개이지만 위에서 부터 동작하는 것을 알 수 있다.

```java
public class DivideByZeroOK {
	public static void main(String[] args) {
		try {
			int [] arr = new int[3];
			arr[3] = 30;
			
			int result = 3 / 0;
			System.out.println("예외를 만나는 순간 캣치행");
			System.out.println(result);
		} 
		catch(ArithmeticException e) {
			//예외처리 안해서 프로그램 죽을 때 그 메시지 출력됨
			e.printStackTrace();
			//발생한 예외의 메시지를 출력
			System.out.println("0으로 나눌 수 없습니다.");
		}
		catch(ArrayIndexOutOfBoundsException e) {
			System.out.println("배열요소 잘못접근");
		}
		System.out.println("정상종료");
	}
}
```

![image](https://user-images.githubusercontent.com/33712866/42674683-bc48dfcc-86ab-11e8-8b0d-8249b4257286.png)



#### finally 블록

오류가 발생하였건 발생하지 않았건 항상 실행되어야 하는 코드는 finally 블록에 넣을 수 있다. (return 하더라도 무조건 실행)

```java
finally {
			System.out.println("여긴 finally");
		}
```

catch 다음에 finally 추가했을 때의 출력결과

![1531460943678](C:\Users\student\AppData\Local\Temp\1531460943678.png)





