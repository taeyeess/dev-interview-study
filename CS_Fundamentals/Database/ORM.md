
## Object-Relational Mapper(ORM)

`ORM`은 Object-Relational Mapper의 약자로, 객체와 RDB 사이의 패러다임 불일치에서 오는 불편함을 해결하기 위해 객체와 RDB를 변환시켜주는 데이터 접근 기술을 말한다.

객체와 관계형 DB를 매핑하여 SQL Query가 아닌 직관적인 형태의 코드(메소드)를 통해 데이터를 조작한다.
> SELECT * FROM user; -> user.findAll();




### 소프트웨어 아키텍처 패턴

<img src="https://github.com/93jpark/dev-interview-study/blob/main/assets/images/db/db_orm_1.png" width="600" height="300">


### Why ORM? 패러다임의 불일치🔥

<img src="https://github.com/93jpark/dev-interview-study/blob/main/assets/images/db/db_orm_2.png" width="600" height="300">


현대의 대부분 어플리케이션 개발은 **객체 지향 언어**를 사용하며, 데이터를 저장하고 관리하기 위해서 데이터베이스, 대부분 **관계형 데이터베이스**를 사용한다. 이 두개의 플랫폼은 서로 다른 패러다임을 지니는데, Java를 이용하는 Spring 프레임워크에서는 데이터를 다룰때 **객체**로 간주하여 프로그래밍한다. 한편, 데이터베이스에서는 **구조화된 테이블**에 대한 쿼리문을 작성하여 데이터를 조작한다. 즉, 각자 지향하는 목적이 다르기 때문에 사용 방법과 표현 방식에 있어 차이가 있을 수 밖에 없다.


### RDB와 OOP 사이의 차이점
| 테이블(RDB)    |   객체(OOP)  |
| :-----: | :---: |
| 변경이 어렵다 | 변경이 쉽다 |
| 모이는 경향(집합) | 분리되는 경향(분해) |
| 데이터 중심 구조 | 추상화, 상속, 다형성 |


- OOP는 객체를 통해 추상화, 캡슐화, 정보은닉, 상속, 다형성 등 다양한 장치를 통해 프로그램을 제어한다.
- RDB는 데이터 정규화를 통해 데이터의 효율적인 저장을 목표로 한다.



#### 상속

```Java
abstract class Person {
    Long id;
    String name;
}

class Employee extends Person {
    String position;
}
```

**슈퍼 타입(Person)** 은 공통 부분을 지니는 특성에 대해 정의하며, **서브 타입(Employee)** 는 공통 속성을 상속받아서 다른 엔티티와 차이가 있는 특성을 지닌다. 

```SQL
INSERT INTO person ...
INSERT INTO employee ...

SELECT p.*, e.*
    FROM person p JOIN employee e
        ON p.id = e.id;
```
위의 Employee객체를 DB에 저장하고 조회하기 위한 SQL은 위와 같다.
Java의 ORM기술인 Hibernate를 사용하면 employee를 조회하기 위한 코드가 다음과 같이 간결해진다.
```JAVA
Employee worker = em.find(Employee.class, empId);
```

#### 연관관계

객체 간의 관계를 나타내는 것이 `연관관계`이다. 객체는 참조(Reference)를 통해 다른 객체와 연관관계를 맺게 되며, 테이블은 외래키를 사용해 다른 테이블과 연관관계를 가지게 된다.

```JAVA
class Employee {
    Long id;
    String position;
    Company employer;
}

class Company {
    Long id;
    String region;
    String name;
}
```
자바에서 객체를 고려하여 엔티티를 설계한다면 위과 같다.

<img src="https://github.com/93jpark/dev-interview-study/blob/main/assets/images/db/db_orm_3.png" width="600" height="300">

하지만 이를 데이터베이스에서 데이터를 저장하기 위해 테이블을 설계한다면 위와 같다.

만약 객체를 테이블의 외래키 참조 형식의 연관관계에 맞추어 재설계한다면 아래와 같은 코드가 나온다.
```JAVA
class Employee {
    Long id;
    Long companyId;
    String position;
}

class Comapny {
    Long id;
    String region;
    String name;
}
```
위와 같은 형식으로 엔티티를 정의하게 된다면, `Compnay employer = employee.getCompany()`와 같은 객체지향적 특징을 사용할 수 없게 된다.

```JAVA
class Employee {
    Long id;
    @ManyToOne @JoinColumn(name="company_id")
    Company employer;
    String position;
}

class Company {
    Long id;
    String region;
    String name;
    @OneToMany(mappedBy="employee_id")
    List<Employee> crews;
}

// CRUD 메소드 예시
empolyee.setCompany(naver);
jpa.persist(employee);

Employee developer = jpa.find(Company.class, id);
Company naver = developer.getEmployer();
```

ORM(JPA:hibernate)를 사용하여 객체의 참조를 어노테이션을 통해 명시해주면 JPA가 해당 객체에 대한 연관관계를 DB의 테이블 기준으로 매핑하여 준다. 개발자는 JPA의 api를 사용하여 객체처럼 메소드를 사용하면 기본적인 CRUD동작 수행이 가능해진다.







### Sql Mapper (MyBatis)

SQL 실행 결과를 자바 빈즈 또는 Map 객체에 매핑하여 Persistence 솔루션으로 관리하며, SQL을 XML파일 형태로 분리한다.
여기서, XML파일로 구분된 SQL문과 프로그래밍 코드를 분리해서 구현한다.