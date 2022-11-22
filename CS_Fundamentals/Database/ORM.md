
## Object-Relational Mapper(ORM)

`ORM`은 Object-Relational Mapper의 약자로, 객체와 RDB 사이의 패러다임 불일치에서 오는 불편함을 해결하기 위해 객체와 RDB를 변환시켜주는 데이터 접근 기술


### 소프트웨어 아키텍처 패턴

<img src="https://github.com/93jpark/dev-interview-study/blob/main/assets/images/db/db_orm_1.png" width="600" height="300">


### Why ORM? 패러다임의 불일치🔥

<img src="https://github.com/93jpark/dev-interview-study/blob/main/assets/images/db/db_orm_2.png" width="600" height="300">



현대의 대부분 어플리케이션 개발은 **객체 지향 언어**를 사용하며, 데이터를 저장하고 관리하기 위해서 데이터베이스, 대부분 **관계형 데이터베이스**를 사용한다. 이 두개의 플랫폼은 서로 다른 패러다임을 지니는데, Java를 이용하는 Spring 프레임워크에서는 데이터를 다룰때 **객체**로 간주하여 프로그래밍한다. 한편, 데이터베이스에서는 **구조화된 테이블**에 대한 쿼리문을 작성하여 데이터를 조작한다. 즉, 각자 지향하는 목적이 다르기 때문에 사용 방법과 표현 방식에 있어 차이가 있을 수 밖에 없다.


- OOP는 객체를 통해 추상화, 캡슐화, 정보은닉, 상속, 다형성 등 다양한 장치를 통해 프로그램을 제어한다.
- RDB는 데이터 정규화를 통해 데이터의 효율적인 저장을 목표로 한다.


`상속 및 연관 관계` <br>

```Java
public class Animal {
    private String name;
    private Long age;
}

public class Human extends Animal {
    private Long SSN;
}

public class Cat exnteds Animal {
    private String tail;
}
```

위와 같이 객체가 정의되어 있다면, 아래와 같이 






### Sql Mapper (MyBatis)

SQL 실행 결과를 자바 빈즈 또는 Map 객체에 매핑하여 Persistence 솔루션으로 관리하며, SQL을 XML파일 형태로 분리한다.
여기서, XML파일로 구분된 SQL문과 프로그래밍 코드를 분리해서 구현한다.