---
layout:     post
title:      "[Spring]AuthController, UserDao"
subtitle:   " \"Java Spring Study\""
date:       2018-07-06 00:00:00
author:     "Jine"
header-img: "img/post-bg-alitrip.jpg"
tags:
    - DB
    - Java
    - Spring
---

ERD

ER은 SQL기반

> ### DB

- nosql
  정형적이지 않을때

- 관계형db
  견고

  



>  ### CRUD

C : CREATE (Table) / INSERT

R : SELECT

U : UPDATE

D : DELETE



ORM -> SQL 몰라도 된다? ㄴㄴ -> 쉽게 사용 가능



SELECT * FROM User WHERE age =>20 AND age <30;

*(요소) / from table  / where뒤에는 조건



> ### JPA

JPA -> Annotation 기반으로 Entity 정의

​	Entity Relation



DB <-------------------------> JPA <--------------------------> Object

AWS / Cloud									AWS

Local DB									Local



InMemory DB(H2)

OAuth2 - token

Redis / Mecached

MSA(Micro Service Architecture)



>  ### ORM

token은 사용기간이 있어서 inMemort DB(cash처럼 휘발성)에 넣는다.
->서버를 껐다키면 록인이 다 풀린다.

MSA 기능단위로 서버를 나눠서 관리
토근을 관리하는 서버를 따로 둠
api는 죽어도 token서버는 죽지않도록!



> #### API - authController

- register

```java
 @Autowired
    private UserDao dao;

    @RequestMapping(value = "/api/auth/register", method = RequestMethod.POST)
    public @ResponseBody TokenModel register(@RequestBody SignUpCommand command) {

        // validate username or password empty
        if (command == null || StringUtils.isEmpty(command.getUsername()) || StringUtils.isEmpty(command.getPassword())) {
            throw new BadRequestException("Please input right username or password");
        }

        String username = command.getUsername();
        String password = command.getPassword();

        // check already username exists.
        if (dao.findByUsername(username).isPresent()) {
            throw new BadRequestException("Already Exists");
        }

        // save to database
        dao.save(new UserEntity(username, password));

        // oauth2
        TokenModel token = new TokenModel("123123", 123123123, "123123123");
        return token;
    }
```

포스트맨

![image](https://user-images.githubusercontent.com/33712866/42421593-f932d16e-8312-11e8-8390-bea63ed55993.png)

토큰이 반환된 것을 볼 수 있다.

![image](https://user-images.githubusercontent.com/33712866/42421604-22c59962-8313-11e8-93d6-1accf8008164.png)

- login

```java
@RequestMapping(value = "/api/auth/login", method = RequestMethod.POST)
public @ResponseBody TokenModel login(@RequestBody SignInCommand command) {

    // validate username or password empty
    if (command == null || StringUtils.isEmpty(command.getUsername()) || StringUtils.isEmpty(command.getPassword())) {
        throw new BadRequestException("Please input right username or password");
    }

    String username = command.getUsername();
    String password = command.getPassword();

    Optional<UserEntity> optionalUser = dao.findByUsernameAndPassword(username, password);
    if (optionalUser.isPresent()) {
        TokenModel token = new TokenModel("123123", 123123123, "123123123");
        return token;
    }

    throw new BadRequestException("Please input the right username or password");
}
```

포스트맨

![image](https://user-images.githubusercontent.com/33712866/42421616-65df1516-8313-11e8-9fc2-aa773a466fc0.png)

잘못입력한 경우

![image](https://user-images.githubusercontent.com/33712866/42421637-ba18ad9a-8313-11e8-965c-9ba31893a62b.png)

> API - USerDao

```java
public interface UserDao extends JpaRepository<UserEntity, Integer> {

    Optional<UserEntity> findByUsername(String username);

    @Query(value = "SELECT * FROM User WHERE username = :username AND password = :password", nativeQuery = true)
    Optional<UserEntity> findByUsernameAndPassword(@Param("username") String username, @Param("password") String password);

}

```

