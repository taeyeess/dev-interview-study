# 자료구조

## Hash 
`Hash`는 키(key)와 값(value)의 쌍으로 저장되는 자료구조를 말한다. 배열에는 여러 키(key)들이 저장되며, 해쉬 함수를 통해 해당되는 값을 가져온다. 키(key)는 중복이 되지 않는 유니크한 값이어야 하며, 값(value)는 중복이 가능하다.

### Hash Table

`해시 테이블`에서 데이터는 유니크한 인덱스 값에 따라 배열의 형태로 저장된다. `해시 함수`는 키 값에 대응되는 해시 테이블의 인덱스를 연산하는 함수를 말한다. 사용자는 키 값을 넣어서 해시 테이블에 저장된 데이터의 위치를 받아 저장된 데이터에 접근할 수 있다.

#### Terminology
| 용어 | 비유 |
| :-: | :-: |
| hash table | 주택단지 |
| bucket | 아파트 |
| 호 | entry |

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

reference: [https://www.youtube.com/watch?v=KyUTuwz_b7Q](https://www.youtube.com/watch?v=KyUTuwz_b7Q)

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

#### Hash Table dynamiclly sizing

load factor = total number of items stores / size of array

Hash Table이 동적으로 늘어날 수 있는 자료구조로 만들고, 저장된 데이터와 테이블 사이즈의 비율(Load Factor)에 따라 hash table 크기 자체를 늘릴 수 있다.
