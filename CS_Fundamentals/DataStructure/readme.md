
# 자료구조

## :memo: Table of Contents

- [배열(Array)](#배열array)
    - [Array 특징](#array의-특징)
    - [Array 단점](#array-단점)
- [연결리스트(Linked List)](#연결-리스트linked-list)
    - [특징](#linked-list의-특징)
    - [단점](#linked-list의-단점)
- [스택(Stack)](#stack)
- [큐(Queue)](#queue)
    - [큐 예시](#que의-사용사례)
- [TCP & UDP](#tcp와-udp)
    - [전송계층](#전송-계층transport-layer)
    - [특징](#특징)
    - [UDP](#udp)
- [Hash](#hash)
    - [hash table](#hash-table)
    - [hash mechanism](#hash-mechanism)
    - [hash table collision](#hash-table-collision)
    - [hash table resizing](#hash-table-dynamiclly-sizing)

<br>

---

<br>

## 배열(Array)

![](https://velog.velcdn.com/images/huunguk/post/d56e1291-5439-4a05-be55-2d61c65e17f5/image.png)

배열은 연속된 메모리 공간에 **순차적으로 저장된 데이터 모음**이다.

배열을 구성하는 각각의 값을 `요소(element)`라고 하며,
배열에서의 위치를 가리키는 숫자는 `인덱스(index)`라고 한다.

배열은 찾고자 하는 원소의 인덱스 값을 알고 있으면 O(1)에 해당 원소로 접근할 수 있다.
즉, **랜덤 엑세스(Random Access)**가 가능하다.

### Array의 특징

- 배열은 논리적인 순서와 물리적인 순서가 같으므로
  **인덱스**를 통해 데이터에 접근할 수 있다.

- 다만 크기가 고정되어 있으므로 크기를 미리 알아야 하고,
  데이터 삽입과 삭제시 `비용(cost)`이 든다.

- 빈 엘리먼트를 허용하고, 중복 엘리먼트가 허용된다.

### Array 단점

배열은 원소를 삽입/삭제하는 과정에서 많은 원소를 이동시켜야 한다.

만약 첫 번째 위치에 새로운 원소를 삽입한다면,
해당 원소에 접근한 뒤(O(1)) 모든 원소들을 한 칸씩 뒤로 `shift` 해야 한다.

반대로 첫 번째 위치의 원소를 삭제한다면,
모든 원소들은 한 칸씩 앞으로 `shift`해줘야 하는 비용과 시간 복잡도가 생긴다.

---

## 연결 리스트(Linked list)

이 부분에 대한 문제점을 해결하기 위한 자료구조가 **linked list**이다.

각각의 원소들은 자기 자신 다음에 어떤 원소인지만 기억을 하고 있으며,
따라서 이 부분만 다른 값으로 바꿔주면 삭제와 삽입을 O(1)만에 해결할 수 있다.

### linked list의 특징

- 항상 **처음 데이터**부터 찾는다.
- 크기가 유동적이므로 크기를 몰라도 되며, 데이터의 삽입과 삭제가 용이하다.
- 빈 엘리먼트를 허용되지 않고(값에 Null은 넣을 수 있음), 중복 엘리먼트가 허용된다.

### linked list의 단점

하지만 원하는 위치에 삽입을 하고자 할 때
원하는 위치를 검색하는 과정에 있어 **첫번재 원소부터** 확인해봐야 한다는 것이다.

`Array`와는 달리 논리적 저장 순서와 물리적 저장 순서가 일치하지 않기 때문이다.
(삽입하고 정렬하는 것과 마찬가지)

이 과정 때문에 어떠한 **원소를 삭제 또는 추가**하고자 했을 때,
그 원소를 찾기 위해 **시간이 추가적으로 발생**하게 된다.

### Summary

결국 linked list 자료구조는 search에도 **time complexity(시간 복잡도)**를 갖고
삽입, 삭제에 대해서도 **time complexity**를 갖는다.

Linked List는 Tree 구조의 근간이 되는 자료구조이며,
Tree에서 사용되었을 때 그 유용성이 드러난다.

<br>

---

<br>

## Stack
- 선형 자료구조. 
- '쌓다'라는 의미
**`Last In First Out(LIFO)` _나중에 들어간 원소가 먼저 나온다._**
![](https://velog.velcdn.com/images/taeyeeya/post/f826c938-f983-4601-8437-48ec01b7c168/image.png)
아래에서 위로 데이터를 차곡차곡 쌓아 올린 형태의 자료구조. 제일 먼저 `stack`에 들어가게 된 원소는 맨 바닥에 깔리게 된다. 
쌓아둔 책을 떠올리면 이해하기가 쉽다. 
제일 밑에 깔린 책 (처음에 들어간 데이터)을 먼저 꺼내기 힘든 것 처럼 가장 마지막에 쌓아 올린 책 (마지막에 삽입된 자료)이 가장 먼저 삭제되는 구조를 가지고 있다. 
정해진 방향으로만 쌓을 수 있으며, top으로 정한 곳을 통해서만 접근 할 수 있다. 
stack에서는 **삽입 연산**을 `push`, 삭제 연산을 `pop`이라고 하며 이러한 스택의 구조를 **후입선출의 구조**라고 한다. 
<br>

### Stack의 사용사례
> - 웹 브라우저 방문기록 (뒤로 가기)
> - 실행 취소 (undo)
> - 역순 문자열 만들기
> - 후의 표기법 계산

<br>

## Queue
- 선형 자료구조.
- Stack과 달리 먼저 들어온 것이 먼저 나가는 선입선출의 구조. 
**`First In Last Out(FILO)` _먼저 들어간 원소가 나중에 나온다._**
![](https://velog.velcdn.com/images/taeyeeya/post/11075005-fe3d-4317-9152-e3ea3e041ce9/image.png)
사람들이 줄 서 있는 곳을 떠올리면, 제일 먼저 카페에 들어온 사람이 제일 먼저 음료를 받고 나가는 것처럼 먼저 삽입 된 자료가 가장 먼저 삭제 되는 구조를 가지고 있다. 
삭제 연산이 수행되는 곳을 프론트(front), 삽입 연산이 이루어지는 곳을 리어(rear)라고 하며, 리어(rear)에서 이루어지는 삽입 연산을 인큐(Enqueue)라고 부르고 프론트(front)에서 이루어지는 삭제 연산을 디큐(dequeue)라고 부른다. 


### Que의 사용사례
>- 은행 업무
>- 대기열 순서와 같은 우선순위의 작업 예약 등 (프린터의 인쇄 대기열)
>- 서비스 센터의 대기 시간
>- 프로세스 관리
>- 게임 대전 매칭 시스템

<br>

---

<br>

## Hash

`Hash`는 키(key)와 값(value)의 쌍으로 저장되는 자료구조를 말한다. 배열에는 여러 키(key)들이 저장되며, 해쉬 함수를 통해 해당되는 값을 가져온다. 키(key)는 중복이 되지 않는 유니크한 값이어야 하며, 값(value)는 중복이 가능하다.

### Hash Table

`해시 테이블`에서 데이터는 유니크한 인덱스 값에 따라 배열의 형태로 저장된다. `해시 함수`는 키 값에 대응되는 해시 테이블의 인덱스를 연산하는 함수를 말한다. 사용자는 키 값을 넣어서 해시 테이블에 저장된 데이터의 위치를 받아 저장된 데이터에 접근할 수 있다.

#### Terminology

|    용어    |   비유   |
| :--------: | :------: |
| hash table | 주택단지 |
|   bucket   |  아파트  |
|   entry     |  호   |

`Hash Function`: 임의 데이터를 고정된 길이의 값으로 리턴해주는 함수
`해쉬, 해쉬값, 해쉬 주소`: 해싱 함수를 통해 리턴된 고정된 길이의 값
`해쉬 테이블`: 키 값의 연산에 의해 직접 접근이 가능한 데이터 구조
`슬롯`: 해쉬 테이블에서 한 개의 데이터를 저장할 수 있는 공간

<img src="https://github.com/93jpark/dev-interview-study/blob/main/assets/images/ds/ds_hash_1.png" width="600" height="300">

### Hash Mechanism

Hashing은 키값을 배열의 인덱스로 변환시키는 기술을 말한다. 가장 쉽게 사용할 수 있는 기술이 나머지연산(modulo)이다. 

##### 기본적인 해시

<img src="https://github.com/93jpark/dev-interview-study/blob/main/assets/images/ds/ds_hash_2.png" width="600" height="300">


이해를 돕기 위해 제한적인 상황에서 (키, 값)들이 해시함수에 의해 해시테이블에 저장되는 과정을 예시로 설명하고자 한다.

오직 26가지의 키값으로 해시테이블을 구성한다면, 해시 테이블은 26개의 인덱스를 가진 배열로 생성된다. 아래는 해시 메커니즘을 순서대로 나열해보았다.

<img src="https://github.com/93jpark/dev-interview-study/blob/main/assets/images/ds/ds_hash_3.png" width="600" height="300">

1. key값은 알파벳 a-z까지 26가지가 존재한다.
2. 각 key값은 아스키코드의 10진법 표현으로 변환된다.
3. 변환된 key값은 Hash함수를 통해 Hash Table의 인덱스로 변환된다.
4. Hash함수는 주어진 정수값을 나머지(modulo)연산을 통해 인덱스 값을 도출하며, 해쉬 테이블의 사이즈인 26을 연산에 사용한다.
5. Hash함수에 의해 도출된 해시테이블 인덱스에 값을 저장한다.

### Hash table Collision

<img src="https://github.com/93jpark/dev-interview-study/blob/main/assets/images/ds/ds_hash_4.png" width="600" height="300">

위의 예시에서는 예외적 상황이 일어날 수 없는 상황을 가정했다. 하지만, 만약 key값의 범주를 모든 캐릭터형으로 바꾸면 일반적인 나머지연산(modulo)으로 해결할 수 없게 된다.

'F'와 'z'의 아스키코드는 각 70과 122이다. 26개 인덱스를 가진 배열을 사용하게 될 경우, 키의 해쉬 함수 결과가 18로 같아지게 된다. 이렇게 되면, 18인덱스에 2개의 값을 저장해야 한다. 이렇게 해시함수가 다른 입력에 대해 같은 출력을 하여, 같은 저장공간(bucket)에 두개 이상의 데이터가 저장되는 경우를 해시 충돌(Hash Collision)이라고 한다. 이를 해결하기 위한 여러 테크닉이 존재한다.

#### Open Addressing

hash table의 주소에 이미 데이터가 저장되어 collision이 일어났을 때, 데이터 저장이 가능한 인접 인덱스에 저장하는 방법을 개방 주소법(open addressing)이라고 한다. 모든 공간이 데이터를 저장할 수 있게 개방되어 있기 때문이다. 

>Reference
(https://www.youtube.com/watch?v=KyUTuwz_b7Q)

#### Separate Chaining
해시 테이블의 저장 공간(bucket)을 LinkedList로 구성하여 해시 충돌을 피하는 기법을 체인 분리법(separate chaining) 또는 폐쇄 주소법(closed addressing)이라고 한다. 이때, LinkedList의 데이터가 저장되는 각 노드를 슬롯(slot)이라고 한다.

- LinkedList라는 부가적인 자료구조를 사용함으로 성능 저하. 충돌이 많아져 리스트가 길어지면 탐색하는데에 O(n)까지 늘어날 수 있음.
- 저장공간의 낭비가 발생
- Open Addressing으로 해결하기엔 데이터가 너무 많아서 Hash Table이 메모리 공간 낭비가 심하다면 고려할 수 있는 기법.

#### Linear Probing 선형 검색법

위의 예시에서 18 인덱스에 이미 데이터가 저장되어 있을 경우, 다시 해시함수를 통해 인덱스를 구해서 비어있는 곳에 저장하는 방법을 선형 검색법(linear probing) 또는 오픈 주소법(open address)이라고 한다. 

- Hash Table의 사이즈가 모자른 경우, load factor에 따라 동적으로 hash table을 늘릴 수 있다.
- 빈 공간을 찾는 탐색과정에서 낭비가 발생할 수 있어 추가 테크닉이 사용될 수 있다.
    - plus 3 rehash, quadratic probing, double hashing .. etc

#### 시간 복잡도

- 일반적인 경우(without collision): O(1)
- worst case(collision): O(n) - 모든 경우에 충돌이 발생하여 LinkedList를 전부 순회해야하거나 HashTable을 모두 순회해야 하는 경우

### Hash Table dynamiclly sizing

load factor = total number of items stores / size of array

Hash Table이 동적으로 늘어날 수 있는 자료구조로 만들고, 저장된 데이터와 테이블 사이즈의 비율(Load Factor)에 따라 hash table 크기 자체를 늘릴 수 있다.
