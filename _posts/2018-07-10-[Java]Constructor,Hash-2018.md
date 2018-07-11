---
layout:     post

title:      "[Java]"

subtitle:   " \"Java Class Day06 2018\""

date:       2018-07-10 09:00:00

author:     "Jine"

header-img: "img/post-bg-2015.jpg"

catalog: true

tags:
    - MultiCampus
    - Java
---

### 생성자

constructor

객체가 생성될때 호출되는 메서드

> ##### 특징

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



궁금한 함수있으면 F3 누르기

##### Hash

- 충돌이 잘 일어나지 않는다.

- 입력은 많아도 출력은 정해져 있다. (커다란게 들어가도 작은게 나온다.)

  ex) 로그인 처리, 나의 아이디 비밀번호를 hash함수에 넣으면 맞다 틀리다만 알 수 있음

  ex) 파일다운로드할때 (SHA-512, 파일을 다운받았을때 나오는 문자열이 일치하면 다운로드를 제대로 받았음을 확인할 수 있다.)

  ex) 비트코인, 블록체인