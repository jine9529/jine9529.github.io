---
layout:     post

title:      "Java Array, Sort Algorithm"

subtitle:   " \"Java Class Day04 2018\""

date:       2018-07-06 09:00:00

author:     "Jine"

header-img: "img/post-bg-2015.jpg"

catalog: true

tags:
    - MultiCampus
    - Java
    - Array
    - Sort

---


### 배열
> ##### 정의

<b>같은 타입 변수들의 모임</b>
<br><br>ex) int[ ] arr;
<br>-> 배열을 기억할 수 있는 위치지정 (위치를 담을 수 있는 변수 arr)
<br>new int[ 10 ];
<br>-> heap 영역에 10칸의 정수공간이 생겨난다.
<br>but, heap영역에서는 이름을 가질 수 없으므로 메모리공간에 위치지정 해놓은 arr이름을 붙인다.
```java
int [] numbers ; //정수배열 데이터의 주소를 담을 수 있는 바구니
numbers = new int [6]; //정수바구니 6개가 모인 배열을 힙 영역에 생성.
				//생성한 데이터(배열)의 주소를 갖다줌
```
<br>

> ##### 왜 사용하는 가

많은 양의 데이터를 변수에 담아둘 필요가 있다면 그 데이터의 크기만큼 바구니가 필요하다.
<br>수많은 데이터를 수동으로 만들면 힘드므로 배열을 사용하여 **같은 타입의 변수**를 **원하는 만큼** 편리하게 한번에 생성 가능하다.
<br>

> ##### 특징

각개로 만들어진 각각의 변수들은 메모리상에 여기저기 산재해서 생성될 수 있다.
<br>반면 같은 배열로 묶인 변수들은 모두 **메모리상에 인접해서 만들**어진다.
<br>

> ##### 주저리주저리

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
![image](https://user-images.githubusercontent.com/33712866/42361057-4fd4a602-8127-11e8-9fc8-488a6d28eef4.png)

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

> ##### 배열의 초기화

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
- 매개변수로 int배열을 받는 add 메서드를 호출하는 경우도 생략불가
```java
int add(int[ ] arr) { /*내용 생략*/ }	//add메서드
int result = add( new int[ ] {100, 90, 80, 70, 60}); //OK
int result = add( {100, 90, 80, 70, 60}); //에러. new int[ ] 생략불가
```
<br>

### 정렬
> ##### 기본

**숫자로 정렬**되어 있으면 자료찾기 수월함
<br>**인덱싱**이 되어있으면 더 빨리 찾을 수 있음

> ##### 정렬예제

첫번째 자리와 뒷숫자들을 비교하고 가장큰수와 자리바꿈
두번째 자리와 뒷숫자들을 비교하고 가장큰수와 자리바꿈
(반복시행 하여 정렬)
```java
public class ArrayPrint {
	public static void main(String[] args) {
		int[] arr = { 5, 3, 7, 2, 8, 1, 4 };

		for (int j = 0; j < arr.length; j++) {
			int max = arr[j];
			int maxIndex = j;
			for (int i = j; i < arr.length; i++) {
				if (max < arr[i]) {
					max = arr[i];
					maxIndex = i;
				}
			}
			int tmp = arr[j];
			arr[j] = arr[maxIndex];
			arr[maxIndex] = tmp;
		}
		for (int a : arr)
			System.out.println(a);
	}
}
```
![image](https://user-images.githubusercontent.com/33712866/42359574-a0f5584c-811d-11e8-9a17-0809aa51ddb4.png)

<br>

> 예제 5-11 빈도수 구하기

```java
public class ArrayCount {
	public static void main(String[] args) {
		int[ ] numArr = new int[10];
		int[ ] counter = new int[10];

		for(int i = 0; i < numArr.length ; i++) {
			numArr[i] = (int)(Math.random()*10);
			System.out.print(numArr[i]);
		}
		System.out.println();

		for(int i=0; i<numArr.length; i++) {
			counter[numArr[i]]++;
		}
		for(int i=0; i<numArr.length; i++) {
			System.out.println(i + "의 개수 :" + counter[i]);
		}
	}
}
```
길이가 10인 배열을 만들고 0과 9사이의 임의의 값으로 초기화한다.
<br>이 배열에 저장된 각 숫자가 몇 번 반복해서 나타나는지를 세어서 배열 counter에 담은 화면을 출력한다.

<br>counter[numArr[i]]++;	// i의 값이 0인 경우를 가정하면,
<br>-> counter[numArr[0]]++;	//numArr[0]의 값은 4이다.
<br>-> counter[4]++;	//counter[4]의 값을 1 증가시킨다.


<br>실행결과
![image](https://user-images.githubusercontent.com/33712866/42359323-1af7a91c-811c-11e8-9e00-ca4a5f24f431.png)

> ##### 버블정렬 (Bubble Sort)

첫번째와 두번째를 보고...두번째가 더 작으면 둘이 바꿔
n-1번째와 n번째를 보고...n번째가 더 작으면 둘이 바꿔
-> 가장 마지막(n번째) 숫자가 정해짐

첫번째와 두번째를 보고...두번째가 더 작으면 둘이 바꿔
n-2번째와 n-1번째를 보고...n-1번째가 더 작으면 둘이 바꿔
-> n-1번째 숫자가 정해짐
(반복)
```java
public class Test {
	public static void main(String[] args) {
		int[] arr = { 5, 3, 7, 2 };

		int tmp = 0;

		for (int j = 0; j < arr.length - 1; j++) {
			for (int i = 0; i < arr.length - 1; i++) {
				if (arr[i] > arr[i + 1]) {
					tmp = arr[i];
					arr[i] = arr[i + 1];
					arr[i + 1] = tmp;
				}
			}
		}
		for (int a : arr)
			System.out.print(a + " ");
	}
}
```
실행결과
![image](https://user-images.githubusercontent.com/33712866/42360419-abf5a0c0-8123-11e8-816c-23b05aec23d6.png)
<br>

> ##### 퀵정렬 (Quick Sort)

계속 부분으로 쪼개서 복잡도를 낮춘다.
<br>한쪽은 피벗보다 작게 한쪽은 피벗보다 크게!

### 2차원 배열

-  NullPointerException

참조변수에 값이 없는데 꾸러미 안에 값을 까보니 없다!
```java
public class Test {
	public static void main(String[] args) {

		int[][] arr = new int[3][];
		arr[0][0] = 10;
		System.out.println(arr.length);
	}
}
```
![image](https://user-images.githubusercontent.com/33712866/42361018-0e4183e0-8127-11e8-841f-ecd982c83516.png)
<br>

> 행렬끼리 덧셈 예제

```java
public class MatrixTest {
	public static void main(String[] args) {
		int[][] matrix1 = {
		{2,3},{4,2}
		};
		int[][] matrix2 = {
		{4,1},{3,7}
		};
		int[][] result = new int[2][2];

		for(int i=0 ;i<matrix1.length; i++) {
			for(int j=0; j<matrix2.length; j++) {
				result[i][j] = matrix1[i][j] + matrix2[i][j];
			}
		}
		for(int i=0; i<2; i++) {
			for(int j=0; j<2; j++) {
				System.out.printf("%3d ", result[i][j]);
			}
			System.out.println();
		}
	}
}
```
실행결과
![image](https://user-images.githubusercontent.com/33712866/42366543-69a70420-813c-11e8-9798-69b05d19f35b.png)

