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


### 배열
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

런타임을 길게 만드는 아이
어레이 아웃 인댁스 아웃


