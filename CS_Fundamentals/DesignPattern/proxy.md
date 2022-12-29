
## Proxy

프록시는 소프트웨어 분야에서 자주 사용되는 용어입니다.

> proxy n. 대리, 위임, 대리인, 대용물

'대리'란 의미로 원래 존재하는 것(origin)이 해야할 일을 대신 시키는 것(delegate)을 의미합니다.

예를 들어, 프록시 서버는 본 서버를 외부에 노출시키지 않고 본 서버의 기능을 모두 갖고 있는 프록시 서버를 서버와 클라이언트 접점에서 본 서버의 역할을 수행하는 것을 말합니다.

### Proxy Pattern

인터페이스를 사용하고 실행시킬 클래스에 대해 객체가 들어갈 자리에 대리자 객체(proxy)를 사용하도록 합니다.

<img src="https://github.com/93jpark/dev-interview-study/blob/main/assets/images/dp/proxy1.png" width="600" height="300">

클라이언트의 입장에서는 메소드를 호출하고 반환 값을 받는 프로세스는 동일합니다.
이 때, 메소드의 실행하는 주체가 정확히 누구인지 상관 할 필요가 없습니다. 또한, 적절한 반환 값을 받는지가 클라이언트의 주된 관심사라고 할 수 있습니다.

위의 그림에서 client는 request()메소드의 실행이 주된 관심입니다.
이 때 RealSubject가 직접 요청을 받는것이 아닌, RealSubject와 같은 인터페이스로 구현된 Proxy객체가 요청을 대신 받고, RealSubject를 호출해서 메소드를 실행하도록 합니다.


### Proxy in Java

```Java
public class Subject {
    String request();
}
```

```Java
public class RealSubject implements Subject {
    @Override
    public String request() {
        return "serve resource along request";
    }
}
```

```Java
public class Proxy implements Subject {
    private final RealSubject realSubejct = new RealSubject();
    private flag cache = false;

    @Override
    public String request() {
        log.info("leave log info about request processing!");
        if(cache==true) {
            return "cache exists!";
        }
            return realSubejct.request();
        
    }
}
```

```Java
public class Main {
    public static void main(String[] args) {
        // Subject 클래스의 메소드를 바로 호출하는 것이 아닌 프록시 클래스의 메소드를 호출
        Subject subject = new Proxy();
        System.out.println(subject.request()); // 내부적으로 Subject의 메소드를 호출
    }
}
```

위의 코드를 통해 다음을 달성할 수 있습니다.
- 인터페이스를 두어 개발코드에서 구현체에 영향을 받지 않는다.
- 구현클래스에 직접 접근하지 않고, Proxy를 통해 우회하여 접근할 수 있다.(흐름의 제어)

* 단, 흐름을 제어하는 것 외에 메소드 처리 과정과 결과에 대한 조작 및 변경은 불가능하다.

### 프록시 패턴의 사용 목적

<img src="https://github.com/93jpark/dev-interview-study/blob/main/assets/images/dp/proxy2.png" width="600" height="300">

<img src="https://github.com/93jpark/dev-interview-study/blob/main/assets/images/dp/proxy3.png" width="600" height="300">

- 흐름제어가 필요한 이유
    - 동기적인 처리를 최대한 비동기적으로 처리하기 위함이다
        위의 예시에서, DB에 대한 요청이 직접 전달되게 되면 병목현상 등이 발생할 수 있다.
        중간에 프록시를 두어서 흐름을 제어하고 DB에 순차적으로 요청이 전달되도록 조절할 수 있다.

    - 실제 메소드가 호출되기 전에 로그처리 및 분산과 같은 전처리를 구현객체의 변경없이 할 수 있다.

    - 캐시를 사용할 수 있다.
        프록시의 내부에 변수 등을 선언하여 데이터가 존재하지 않는 경우와 존재하는 경우로 나누어 흐름을 제어할 수 있다.