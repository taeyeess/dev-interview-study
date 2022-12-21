

<br>

---

<br>

## Builder 빌더 패턴

`빌더패턴`은 객체를 생성하는 것과 표현하는 것을 분리하여, 서로 다른 표현이라도 이를 생성할 수 있는 동일한 절차를 제공하는 패턴을 말한다. 이 생성 패턴(creational pattern)은 객체의 속성이 선택적(optional)인 항목이 많을 수록 빛을 발휘한다.

> 다른 생성 패턴으로는 싱글톤, 팩토리, 추상 팩토리 등이 존재한다.

### 생성자를 통한 인스턴스화 (Instatiate)

```Java
class Member {
    private String name;     // required
    private String email;    // required
    private String password; // required
    private String SSN;      // required
    private String region;
    private String age;
    private String job;

    public Member(String name, String email, String password, String SSN, String region, String age, String job) {
        this.name = name;
        this.email = email;
        this.password = password;
        this.SSN = SSN;
        this.region = region;
        this.age = age;
        this.job = job;
    }
}
```

Member클래스의 생성자를 보면 Member 객체를 인스턴스화하기 위해서 많은 값들을 받아옵니다. 또한, 몇개의 필드는 필수항목이며, 나머지는 선택적으로 받을 수 있습니다.

```Java
Member newMember = new Member("Joon", "93jpark@gmail.com", "p@ssw0rd", "931023", "Busan", "30", "Unemployed");

Member otherMember = new Member("Woogie", "woogie@gmail.com", "qwer1234", null, null, null, null);
```

자바에서는 위의 코드처럼 클래스의 생성자를 통해 인스턴스화를 이룹니다. newMember는 모든 필드를 채우며 객체를 생성하지만, otherMember는 몇개의 항목을 제외하며 생성됩니다.
이때, 코드의 가독성이 매우 떨어짐을 알 수 있습니다. otherMember를 생성할 때 null값으로 전달되는 것이 어떤 항목에 대한 값인지 알기 어렵습니다.

### 점층적 생성자 패턴(Telescoping Constructor Pattern)

위의 기본적인 인스턴스화에서 발생하는 문제를 보완하기 위해 `점층적 생성자 패턴`을 사용할 수 있습니다.

```Java
public Member(String name, String email, String password, String SSN) {
    this.name = name;
    this.email = email;
    this.password = password;
    this.SSN = SSN;
    this.region = null;
    this.age = null;
    this.job = null;
}

public Member(String name, String email, String password, String SSN, String region) {
    this.name = name;
    this.email = email;
    this.password = password;
    this.SSN = SSN;
    this.region = region;
    this.age = null;
    this.job = null;
}

public Member(String name, String email, String password, String SSN, String region, String age) {
    this.name = name;
    this.email = email;
    this.password = password;
    this.SSN = SSN;
    this.region = region;
    this.age = age;
    this.job = null;
}

public Member(String name, String email, String password, String SSN, String region, String age, String job) {
    this.name = name;
    this.email = email;
    this.password = password;
    this.SSN = SSN;
    this.region = region;
    this.age = age;
    this.job = job;
}
```

클래스의 생성자를 파라미터의 케이스에 따라서 모두 정의하는 방법입니다.
첫번쨰 생성자를 사용하여 인스턴스화를 하는 방법에 비하면 그나마 괜찮은 방법이지만,
모든 경우에 대해 생성자를 정의해야하기때문에 깔끔한 방법은 되지 못합니다.

### 자바 빈 패턴(JavaBeans Pattern)

`자바 빈 패턴`은 객체를 먼저 생성하고, 멤버 변수를 나중에 초기화시킵니다.
생성자의 영향을 받지 않기 때문에 생성자를 많이 구현할 필요가 없습니다.

```Java
public class Member {

    private String name;     // required
    private String email;    // required
    private String password; // required
    private String SSN;      // required
    private String region;
    private String age;
    private String job;
    

    public void setName(String name) {
        this.name = name;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    // ...

}
```

위의 Setter를 활용하여 객체를 설정하는 방법은 다음과 같습니다.

```Java
Member newMember = new Member();
newMember.setName("Joon");
newMember.setEmail("93jpark@gmail.com");
// ...
```

이러한 방식의 단점은 멤버 변수를 초기화하는데에 여러번의 setter메소드를 호출해야하며, 객체의 불변성에 대해 보장할 수 없습니다.

### 빌더 패턴
위의 자바빈즈 패턴을 극복하기 위해 고안된것이 빌더 패턴입니다.
새로운 객체가 필요한 곳에서 직접 생성하기 전에 필수 인자 값들을 전달하여 빌더 객체를 생성한 후 빌더 객체에 정의된 메소드를 호출하여 객체를 생성하는 것입니다.

```Java
class Member {
    private String name;     // required
    private String email;    // required
    private String password; // required
    private String SSN;      // required
    private String region;
    private String age;
    private String job;

    Member(Builder builder) {
        this.name = builder.name;
        this.email = builder.email;
        this.password = builder.password;
        this.SSN = builder.SSN;
        this.region = builder.region;
        this.age = builder.age;
        this.job = builder.job;
    }

    public static class Builder {
        private String name;     // required
        private String email;    // required
        private String password; // required
        private String SSN;      // required
        private String region;
        private String age;
        private String job;

        public Builder(String name, String email, String password, String SSN) {
            this.name = name;
            this.email = email;
            this.password = password;
            this.SSN = SSN;
        }

        public Builder region(String region) {
            this.region = region;
            return this;
        }

        public Builder age(String age) {
            this.age = age;
            return this;
        }

        public Builder job(String job) {
            this.job = job;
            return this;
        }

        public Member build() {
            return new Member(this);
        }
    }

}

```

Member 클래스 내부에 정적 클래스인 Builder를 정의합니다.
그리고, Builder클래스는 각 멤버 변수의 setter에 해당하는 메소드를 지니고 있습니다.
따라서 Member클래스는 내부의 Builder를 통해 멤버 변수가 설정되고 객체가 생성되게 됩니다.

```Java
Member newMember = new Member.Builder("Joon", "93jpark@gmail.com", "p@ssw0rd", "931023")
                                .region("busan")
                                .age("30")
                                .job("unemployed")
                                .build();
```
