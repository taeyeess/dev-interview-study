# 콜백함수(Callback Function)
- 함수를 활용하는 방법중 하나
- 정확하게는 콜백함수는 파라미터로 전달받은 함수를 말한다
- 파라미터로 콜백함수를 전달받고 함수 내부에서 필요할 때 콜백함수를 호출할 수 있다.
- 간단히 말해 **함수 안에서 실행하는 또 다른 함수**
- 다른 함수가 실행을 끝낸 뒤 실행되는 callback (다시 불러오는?)함수를 말한다. 
그리고 함수를 만들 때, **parameter를 함수로 받아서 쓸 수 있는데 그 함수는 callback**이다. 

- 자바스크립트에서 함수는 다른 함수의 인자로 쓰일 수도 있고, 어떤 함수에 의해 리턴될 수도 있다. **결국 인자로 넘겨지는 함수를 콜백함수**라고 한다. 
또한 단지 **함수를 등록하기만 하고 어떤 이벤트가 발생했거나 특정 시점에 도달했을 때 시스템에서 호출하는 함수를 콜백함수**라고 한다. 

```javascript
function introduce (lastName, firstName) {
	return lastName + firstName;
}

fuction printResult(result) {
	console.log(reuslt)
}

printResult(introduce("김", "태이"))

```
lastName과 firstName을 인자로 받아서 합친 결과를 return해주는 `introduce` 함수를 선언하고, 파라미터를 받아 콘솔로 찍어주는 `printResult` 함수가 있을때 `printResult` 함수의 파라미터로 `introduce`함수를 받아 인자로 "김", "태이"를 넘겨주면 "김"과 "태이"가 합쳐진 "김태이"가 콘솔창에 찍힌다. 

위의 코드를 콜백함수로 구현하면 다음과 같이 변경할 수 있다.


```javascript
function introduce(lastName, firstName, print) {
	print(lastName + firstName);
}

function printResult(result) {
	console.log(result)
}

introduce("김", "태이"
, printReult)
```

![](https://velog.velcdn.com/images/taeyeeya/post/163a7cb5-7086-4b5d-b49d-5f087700a3d2/image.png)
`introduce` 함수에 콜백함수를 받을 `print` 라는 파라미터를 추가하고 내부에서 lastName과 firstName의 합을 인자로 전달해 주고, `print` 파라미터의 인자로 `printResult` 함수를 전달해주었다. 
먼저 `introduce` 함수가 호출된 후 `printResult` 함수가 `introduce` 함수 내부에서 나중에 호출되게 된다.
여기서 `printResult` 함수가 바로 **콜백함수** 이다.


또한 콜백함수는 정의된 함수 뿐만 아니라 **익명함수**도 인자로 전달할 수 있다.

```javascript
function introduce(lastName, firstName, print) {
	print(lastName + firstName);
}

introduce("김", "태이", (result) => {
	console.log(result)
})
```

### 콜백함수를 이용한 비동기처리
콜백함수는 주로 비동기처리에 사용되는데, 
**비동기(Asynchronous)** 란 특정 코드의 실행이 끝날 때 까지 기다리지 않고 다음 코드로 바로 넘어가는 것을 의미합니다. 
대표적으로 자바스크립트에 내장되어 있는 `setTimeout()`이라는 함수가 있습니다. 


```javascript
function callBackTestFunc(callback) {
	setTimeout(callback, 1000)
  	console.log('Hello')
}

callBackTestFunc(() => {
	console.log('waited 1 second')
})
```

```javascript
Hello
waited 1 second
```

`callback` 이라는 파라미터를 선언하고 콜백함수를 전달 받아 `setTimeout()` 함수의 인자로 전달하였습니다.

`setTimeout()` 함수는 **비동기 함수**이기 때문에 코드의 실행이 끝날 때 까지 기다리지 않고 바로 다음코드로 넘어갑니다.

그렇기 때문에 **Hello**가 먼저 출력되고 **1(1000ms)초** 뒤에 콜백함수가 실행 되는 것입니다.


### 콜백함수의 장단점
콜백함수를 사용하면서 얻는 이점은 다음과 같습니다. 
- 함수를 인자로 받기 때문에 필요에 따라 함수의 정의를 달리해 전달할 수 있습니다. 
- 함수를 굳이 정의하지 않고 익명 함수로도 전달 가능합니다. 
- 비동기(Asynchronous)처리 방식의 문제점을 해결할 수 있습니다.

하지만 콜백함수를 사용하면 다음과 같은 단점이 있습니다. 
- 콜백함수를 너무 남용하면 코드의 가독성이 떨어집니다. (콜백지옥)
- 에러 처리가 어렵다. 



<br>


#### 참고 사이트
- https://yoo11052.tistory.com/153
- https://bigtop.tistory.com/35
 
- https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%BD%9C%EB%B0%B1-%ED%95%A8%EC%88%98

- https://velog.io/@ko1586/Callback%ED%95%A8%EC%88%98%EB%9E%80-%EB%AD%94%EB%8D%B0

