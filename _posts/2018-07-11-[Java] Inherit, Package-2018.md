---
layout:     post

title:      "[Java]inheritance"

subtitle:   " \"Java Class Day07 2018\""

date:       2018-07-11 09:00:00

author:     "Jine"

header-img: "img/post-bg-2015.jpg"

catalog: true

tags:
    - MultiCampus
    - Java
---

VCM

<정보관리분야>

| 정보관리분야 |                      |                       | 데이터분석분야    |
| :----------- | -------------------- | --------------------- | ----------------- |
| View         | 프런트엔드, 퍼블디셔 | HTML, CSS, JavaScript | 시각화            |
| Controller   | 백엔드, 웹서버       | Java                  | MapReduce병렬처리 |
| Model        | DBMS                 | oracle                | HDFS 하둡....~~   |



## 상속

Day06에 했던 Circle과 Point는 포함관계 -> has a 관계

employee와 person은 상속관계 -> is a 관계



자식클래스가 부모에 정의되어있는 변수나 함수를 다시 더 만들면?

```java
class Parent{
	int data=100;
	public void print() {
		System.out.println("Parent의 data : " + data);
	}
}

class Child extends Parent{
	int data = 200;
	public void print() {
		System.out.println("Child의 data :" + data);
		System.out.println("this.data :" + this.data);
		System.out.println("super.data :" + super.data);
	}
}

public class Test {
	public static void main(String[] args) {
		Child c = new Child();
//		c.data = 10;
		c.print();
	}

}
```

![image](https://user-images.githubusercontent.com/33712866/42545550-a37818b4-84f3-11e8-9baa-34ade34461ad.png)

##### 오버라이딩

부모클래스가 정의 한 멤버변수, 멤버함수는 어차피 자식도 갖고 있지만,

 자식이 다시 또 만드는 것을 '오버라이딩' 이라고 부릅니다.

##### 중요

자식클래스가 객체화 될때는 부모클래스의 기본생성자를 묵시적으로 호출한다.

부모클래스가 기본 생성자가 없다면 자식클래스의 생성자 첫줄에서 부모클래스의 생성자를 명시적으로 호출한다.



## 패키지

클래스들을 묶은 것



다른 패키지의 클래스를 사용하시 위해서는 

- 풀네임으로 부르기
- import 패키지



##### 날짜 출력

```java
import java.util.Date;
import java.text.SimpleDateFormat;

public class ImportTest {
	public static void main(String[] args) {
		Date today = new Date();

		SimpleDateFormat date = new SimpleDateFormat("yyyy/MM/dd");
		SimpleDateFormat time = new SimpleDateFormat("hh:mm:ss a");
		
		System.out.println("오늘 날짜는 " + date.format(today));
		System.out.println("현재 날짜는 " + time.format(today));
	}
}
```

![image](https://user-images.githubusercontent.com/33712866/42547922-6cddb67c-84ff-11e8-81da-4c3afb03a1c0.png)

##### import 

ex) 시간

```java
import java.util.Date;
import java.text.SimpleDateFormat;

public class ImportTest {
	public static void main(String[] args) {
		Date today = new Date();

		SimpleDateFormat date = new SimpleDateFormat("yyyy/MM/dd");
		SimpleDateFormat time = new SimpleDateFormat("hh:mm:ss a");
		
		System.out.println("오늘 날짜는 " + date.format(today));
		System.out.println("현재 날짜는 " + time.format(today));
	}
}
```



##### wrapper

```java
import java.util.Scanner;

public class Wrapper {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		
		System.out.println("숫자를 입력해주세요.");
		String a = scan.nextLine();
		System.out.println("숫자를 입력해주세요.");
		String b = scan.nextLine();
		
		int x = Integer.parseInt(a);
		int y = Integer.parseInt(b);
		
//		int z = x + y;
		System.out.println("두 수의 합은 "+ (x+y) + "입니다.");
		
	}

}
```

##### StringTokenizer

```java
import java.util.StringTokenizer;

public class StrintTest {
	public static void main(String[] args) {
		StringTokenizer st = new StringTokenizer("will Java change my life?");
		while (st.hasMoreTokens()) {
			System.out.println(st.nextToken());
		}
	}
}
```

![image](https://user-images.githubusercontent.com/33712866/42550857-103bcf48-850f-11e8-833c-2f67c4695150.png)

##### StringTokenizer 식입력받아 결과출력

```java
import java.util.Scanner;
import java.util.StringTokenizer;

public class StrintTest {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		System.out.println("식을 입력해주세요");
		String line = scan.nextLine();

		StringTokenizer st = new StringTokenizer(line, "+");

		int result = 0;
		
		while (st.hasMoreTokens()) {
			int num = Integer.parseInt(st.nextToken());
			result += num;
		}
		System.out.println("결과는 " + result);
	}
}
```

![image](https://user-images.githubusercontent.com/33712866/42551734-b8a80c6a-8513-11e8-97ca-58991f52aa0a.png)

##### 동적할당없이 계좌예제

```java
package bank;

import java.util.Scanner;

public class BankApp {
	public static void main(String[] args) {
		Account[] account = new Account[100];
		int accountCount = 0;
		
		Scanner scan = new Scanner(System.in);
		int userSel = -1;

		while (true) {
			System.out.println("1. 계좌생성");
			System.out.println("2. 입금");
			System.out.println("3. 출금");
			System.out.println("4. 이체");
			System.out.println("5. 계좌조회");
			System.out.println("0. 종료");
			userSel = Integer.parseInt(scan.nextLine());

			if (userSel == 1) {
				System.out.println("계좌번호를 입력하세요");
				String id = scan.nextLine();
				account[accountCount] = new Account();
				account[accountCount].setId(id);
				System.out.println("이름을 입력하세요");
				String name = scan.nextLine();
				account[accountCount].setOwner(name);
				account[accountCount].setBalance(0);
							
				System.out.println("계좌번호 : " + account[accountCount].getId());
				System.out.println("계좌주 : " + account[accountCount].getOwner());
				accountCount++;
			} 
			
			else if (userSel == 2) {
				System.out.println("조회할 계좌주를 입력하세요");
				String wantName = scan.nextLine();
				for(int i=0; i<accountCount; i++) {
					if(wantName.equals(account[i].getOwner())){
						System.out.println("당신의 잔액은 " + account[i].getBalance() + "입니다.");
						
						System.out.println("입금할 금액을 입력하시오.");
						int money = Integer.parseInt((scan.nextLine()));
						account[i].setBalance(account[i].getBalance() + money);		
						
						System.out.println("입금성공");
						System.out.println("당신의 잔액은 " + account[i].getBalance() + "입니다.");
						break;
					}
				}
			} 
			
			else if (userSel == 3) {

				System.out.println("조회할 계좌주를 입력하세요");
				String wantName = scan.nextLine();
				for(int i=0; i<accountCount; i++) {
					if(wantName.equals(account[i].getOwner())){
						System.out.println("당신의 잔액은 " + account[i].getBalance() + "입니다.");
						
						System.out.println("출금할 금액을 입력하시오.");
						int money = Integer.parseInt((scan.nextLine()));
						if( account[i].getBalance()<money)
							System.out.println("출금을 할 수 없습니다. 잔액부족");
						else {
							account[i].setBalance(account[i].getBalance() - money);		
							
							System.out.println("출금성공");
							System.out.println("당신의 잔액은 " + account[i].getBalance() + "입니다.");
							break;
						}
					}
				}
			} 
			
			else if (userSel == 4) {
				System.out.println("송금할 계좌의 계좌주를 입력하세요");
				String sandName = scan.nextLine();
				
				System.out.println("송금받을 계좌의 계좌주를 입력하세요");
				String receiveName = scan.nextLine();
				
				for(int i=0; i<accountCount; i++) {
					if(sandName.equals(account[i].getOwner())){
						System.out.println("당신의 잔액은 " + account[i].getBalance() + "입니다.");
						
						System.out.println("송금할 금액을 입력하시오.");
						int money = Integer.parseInt((scan.nextLine()));
						
						if(account[i].getBalance() < money) {
							System.out.println("돈이 없습니다. 조금만 보내세요.");
							continue;
						}
						
						account[i].setBalance(account[i].getBalance() - money);		
						
						for(int j=0; j<accountCount; j++) {
							if(receiveName.equals(account[i].getOwner())) {
								System.out.println("계좌가 확인되었습니다.");
								account[j].setBalance(account[j].getBalance() + money);				
							}
						}
					
						System.out.println("이체성공");
						System.out.println("당신의 잔액은 " + account[i].getBalance() + "입니다.");
						break;
					}
				}
			}
			
			else if (userSel == 5) {
				System.out.println("조회할 계좌주를 입력하세요");
				String wantName = scan.nextLine();
				for(int i=0; i<accountCount; i++) {
					if(wantName.equals(account[i].getOwner())){
						System.out.println("계좌번호 : " + account[i].getId());
						System.out.println("계좌주 : " + account[i].getOwner());
						System.out.println("당신의 잔액은 " + account[i].getBalance() + "입니다.");
						break;
					}
				}

			} 
			else if(userSel == 0)
				break;
			else
				System.out.println("그런 메뉴 없어요. 다시입력해주세요.");
		}
	}
}

```



[파이썬공부](http://nbviewer.jupyter.org/gist/FinanceData/69c17208fa55d2285a2560c3d7972876)

