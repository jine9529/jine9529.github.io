---

layout:     post

title:      "Java Class Day04 2018"

subtitle:   " \"MultiCampus\""

date:       2018-07-06 09:00:00

author:     "Jine"

header-img: "img/post-bg-2015.jpg"

catalog: true

tags:
    - MultiCampus
    - Java

---


###배열
> 정의

<b>같은 타입 변수들의 모임</b>
<br><br>ex)int[ ] arr;
<br>-> 배열을 기억할 수 있는 위치지정 (위치를 담을 수 있는 변수 arr)
<br>new int[ 10 ];
<br>-> heap 영역에 10칸의 정수공간이 생겨난다.
<br>but, heap영역에서는 이름을 가질 수 없으므로 메모리공간에 위치지정 해놓은 arr이름을 붙인다.
```java
int [] numbers ; //정수배열 데이터의 주소를 담을 수 있는 바구니
numbers = new int [6]; //정수바구니 6개가 모인 배열을 힙 영역에 생성.
						//생성한 데이터(배열)의 주소를 갖다줌
```

> 왜 사용하는 가

<br>많은 양의 데이터를 변수에 담아둘 필요가 있다면 그 데이터의 크기만큼 바구니가 필요하다.
<br>수많은 데이터를 수동으로 만들면 힘드므로 배열을 사용하여 **같은 타입의 변수**를 **원하는 만큼** 편리하게 한번에 생성 가능하다.
<br>

> 특징

각개로 만들어진 각각의 변수들은 메모리상에 여기저기 산재해서 생성될 수 있다.
<br>반면 같은 배열로 묶인 변수들은 모두 **메모리상에 인접해서 만들**어진다.
<br>

> 주저리주저리

- 배열이름**.**length
```java
int [ ] arr = new int [5];
int tmp = arr.length;
```

- ArrayIndexOutOfBoundsException 예외
배열의 인덱스가 유효한 범위를 벗어났다는 에러
```java
int [] score = new int [5];
for (int i = 0; i<6; i++) { //실수로 조건식을 변경하지 않음
	System.out.println(score[i]); //에러발생!
}
```
배열의 길이가 변경되면 for문 조건의 범위도 변경해야 하지만 잊고 실행한다면
<br>for문은 배열의 유요한 인덱스 범위인 0~4를 넘어 5까지 반복하기 때문에
5번째에서 ArrayIndexOutBoundsException 예외가 발생하여 비정상적으로 종료된다.

 - 해결 (score.length 사용)
 ```java
 int [] score = new int [5];
 for(int i=0; i<score.length; i++){
 	System.out.println(score[i]);
 }
 ```
<br>

> 배열의 모든 요소 출력 예제

```java
1. for(int i =0; i < arr.length; i++)
	System.out.println(arr[i]);
2. for(int a: arr)
    System.out.println(a);
```
2번은 arr 배열에 담긴 요소들은 int a 자리에 하나씩 넣어 출력하는 것이다.
<br>

> 배열의 초기화

- 배열의 생성과 초기화를 동시에 하는 경우에는 new int[ ] 생략가능
```java
int[ ] score = new int[ ]{50, 60, 70, 80, 90};
int[ ] score = {50, 60, 70, 80, 90}; // new int[ ]생략가능
```
- 배열의 선언과 생성을 따로하는 경우에는 생략불가
```java
int[ ] score;
score = new int[ ]{50, 60, 70, 80, 90}; //OK
score = {50, 60, 70, 80, 90}; //에러. new int[ ]생략불가
```
-매개변수로 int배열을 받는 add 메서드를 호출하는 경우도 생략불가
```java
int add(int[ ] arr) { /*내용 생략*/ }	//add메서드
int result = add( new int[ ] {100, 90, 80, 70, 60}); //OK
int result = add( {100, 90, 80, 70, 60}); //에러. new int[ ] 생략불가
```