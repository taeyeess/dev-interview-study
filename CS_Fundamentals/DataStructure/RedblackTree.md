## 레드 블랙 트리
***

![image](https://velog.velcdn.com/images%2Fmain_door%2Fpost%2F84678409-1a8e-4325-b45c-07a57f2cc814%2Fimage.png) 
<br>
* 이진 탐색 트리의 한 종류
* 스스로 균형잡는 트리
* BST의 worst case의 단점을 개선
* 모든 노드는 red or black

>대표적으로 연관 배열 등을 구현하는데 쓰이는 자료구조.
숫자 등의 비교 가능한 자료를 정리하는 데 쓰이는 자료구조



>레드 블랙 트리를 사용하는 이유
-이진 탐색 트리의 단점을 보완하기 위해서 쓰는 자료구조.
-루트 노드부터 가장 먼 리프 노드까지의 거리가, 가장 가까운 노드 경로까지의 거리의 두 배 보다 항상 작다는 특성 때문에


***

###red-black트리의 속성

1. 모든 노드는 red or black
2. 루트 노드는 black
3. 모든 nil 노드는 black
4. red의 자녀들은 black or red가 연속적으로 존재할 수 없다.
5. 임의이 노드에서 자손 nil노드들까지 가는 경로들의 black 수는 같다.(자기 자신은 count에서 제외)
 * 5번 속성 특징
  -RB트리가 5번 속성을 만족하고 있고, 두 자녀가 같은 색을 가질 때 부모와 두 자녀의 색을 바꿔줘도 5번 속성은 여전히 만족된다.
  <br>
  


 * nil 노드란?
    -존재하지 않음을 의미하는 노드
    -자녀가 없을 때 자녀를 nil 노드로 표기
    -값이 있는 노드와 동등하게 취급
    -RB 트리에서 leaf 노드는 nil 노드
<br>
* 노드 x의 black height
    -노드 x에서 임의의 자손 nil 노드까지 내려가는 경로에서의 black 수(자기 자신은 count에서 제외)
    -5번 속성을 만족해야 성립하는 개념

***
cf) https://www.cs.usfca.edu/~galles/visualization/RedBlack.html

##삽입

* ##### 새로 삽입되는 노드는 red
* ##### case1 : 부모 노드가 레드인데, 부모의 형제가 없거나 블랙일 때 - 회전
* ##### case2 : 부모 노드가 레드인데, 부모의 형제가 레드일 때 - 색상 변환( 5번 속성 특징 이용) 

 <br>
  
    
![image](https://mblogthumb-phinf.pstatic.net/MjAxODAzMThfNDMg/MDAxNTIxMzczMjI4MTYy.9AcFMeiSqwhRzQ8TOaQsM-dAlcKjL8ySdEtL1GIXVecg.jS9fbDqs-BaSbh4QouHENAt6NvZQioluqPWQF2vf2_Ug.PNG.min-program/%25EC%258A%25AC%25EB%259D%25BC%25EC%259D%25B4%25EB%2593%259C03.png?type=w800)   
##### 루트노드 20인 상태에서 15가 들어오면 이진 탐색 트리의 특징에 따라 20의 왼쪽 자식으로 삽입. 현재 RB트리의 속성을 모두 만족함으로 다음 노드 삽입
![image](https://mblogthumb-phinf.pstatic.net/MjAxODAzMThfMjk0/MDAxNTIxMzczMjI4MTYz.3fgjVJStTbl1OEygEtikap5pLsORb2k9ttYKrK1sl4Yg.jwu7DnspNdSo9iaTk0-2trwRnwQdsPK5CIqiUX8xECYg.PNG.min-program/%25EC%258A%25AC%25EB%259D%25BC%25EC%259D%25B4%25EB%2593%259C04.png?type=w800) 

##### red가 연속적으로 붙어있는 문제 발생 -> 이때 위의 2가지 case를 생각해볼 수 있는데, 현재 삽입된 노드의 부모 노드가 레드이고, 부모의 형제가 없으므로 case1에 따라 회전을 한다. 또한, 자리가 바뀌는 노드의 경우 원래 그자리에 있었던 노드의 색상을 가진다.(부모 노드와 할아버지 노드의 색상을 바꾼 뒤 회전한다 생각하면 이해하기 쉽다.)

![image](https://mblogthumb-phinf.pstatic.net/MjAxODAzMThfNTYg/MDAxNTIxMzczMjI4MDY5.8DNGTN9RQ7wCazEUTRbmTufTU76dir3q5xionwB8JYMg.uigy5vJaxqbt45l0jvN525e6IOGshhp8u5-ZucKcj-8g.PNG.min-program/%25EC%258A%25AC%25EB%259D%25BC%25EC%259D%25B4%25EB%2593%259C05.png?type=w800)

##### 회전 후 모습
![image](https://mblogthumb-phinf.pstatic.net/MjAxODAzMThfMTk5/MDAxNTIxMzczNDYyMTM3.kXPTDqDnoO645xcFPrbI-YJh4R83Veiy1vXAaaQdursg.eAHQeAf-9WqmfSCvSvk3lNnHcRaqAPhjd4xstkXJojEg.PNG.min-program/%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%93%9C07.png?type=w800)

##### RB트리 속성 모두 만족했으므로 다음 노드 12 삽입, 부모노드가 레드이고, 부모의 형제 노드도 레드인, case2 의 경우이므로 색상을 전환해준다. 이때 위의 5번 속성 특징(RB트리가 5번 속성을 만족하고 있고, 두 자녀가 같은 색을 가질 때 부모와 두 자녀의 색을 바꿔줘도 5번 속성은 여전히 만족된다)을 이용한다. 
![image](https://mblogthumb-phinf.pstatic.net/MjAxODAzMThfMjEy/MDAxNTIxMzczNjQwMjQ3.TAu7Wj5IcWKYJ2L73sbNfSvy48wjtPS2CM20BTalva0g.4KtQu_pFIAsJU0QyjvnKngOc9FP4gfmqDCy_a4JbDqwg.PNG.min-program/%25EC%258A%25AC%25EB%259D%25BC%25EC%259D%25B4%25EB%2593%259C08.png?type=w800)

##### 색상 전환 후 모습
![image](https://mblogthumb-phinf.pstatic.net/MjAxODAzMThfMjIg/MDAxNTIxMzczNjQwMjQy.BZssXmP4_KD81Pnwz1T39ttqpT2bnJmBVt0BfMDfGZcg.T6K1KHM1VAdzyX-BX-xtGGAH6eXS9QFJc7tGQfIb7ZIg.PNG.min-program/%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%93%9C10.png?type=w800)

##### 다음 노드 5 삽입, case1의 회전 필요
![image](https://mblogthumb-phinf.pstatic.net/MjAxODAzMThfMjA5/MDAxNTIxMzczODkwNDcz.46EsLSNnuR0CTgba2B9qtCsYpFRREKoZmrOcDQAIn1Mg.qaRVxc0Cidjh7lZgRzOKdIOaFcyaEshMWK4mGXXQyxAg.PNG.min-program/%25EC%258A%25AC%25EB%259D%25BC%25EC%259D%25B4%25EB%2593%259C11.png?type=w800)

##### 이렇게 할아버지 노드부터 자식 노드까지 꺾여있는 경우 먼저 일직선으로 만들어준 뒤 회전한다. 12를 기준으로 오른쪽으로 회전하여 3-5-12 일직선으로 만들어 주고, 부모와 할아버지의 노드 색상을 변경한 뒤 왼쪽으로 회전한다.
![image](https://mblogthumb-phinf.pstatic.net/MjAxODAzMThfMTE3/MDAxNTIxMzczODkwNDQz.GB0FLvjPcf4-MvAXE4Q8v2v5PfEmRBhPqC9GoLTqAYgg.4Xae8-jG9RZbbls4LDeuHI-AnG0R15QzVyvcPIqcJMkg.PNG.min-program/%25EC%258A%25AC%25EB%259D%25BC%25EC%259D%25B4%25EB%2593%259C13.png?type=w800)

출처 : https://m.blog.naver.com/min-program/221231697752
***
## 삭제
 ##### 삭제되는 색을 통해 속성 위반 여부 확인
* 삭제하려는 노드의 자녀가 없거나 하나라면 삭제되는 색은 삭제되는 노드의 색
* 삭제하려는 노드의 자녀가 둘이라면 삭제되는 색은 삭제되는 노드의 successor의 색
* 삭제되는 색이 red라면 어떠한 속성도 위반하지 않는다.
* 삭제되는 색이 black일때 대부분의 경우에는 5번 속성을 위반하게 된다.

##### 삭제되는 색이 black이고, 5번 속성 위반일 때
* 경로에서 black수를 카운트할 때 extra black은 하나의 black으로 카운트 된다.
* 삭제된 색의 위치를 대체한 노드인 nil노드에 extra black을 부여하면 5번 속성을 다시 만족한다.
* doubly-black: extra black이 부여된 black노드
* Red-and-Black: extra black이 부여된 red노드

## red and black 해결하기
* red-and-black을 black으로 바꾸면 해결

![image](https://velog.velcdn.com/images/youngcheon/post/361155b1-f838-48c6-9231-3399e176480f/image.png)

* 30은 자녀가 하나이므로, 삭제되는 색은 삭제되는 노드의 색 black.
* 30을 대체하는 25의 red에 extra black 부여
* 25가 red-and-black 되었으니 25를 black으로 바꿔주면 종료 

## doubly-black 해곃하기

* extra black을 어떻게 없앨건지가 관건
* 네가지 case로 분류할 때의 기준은 doubly-black의 형제의 색과 그 형제의 자녀들의 색

### case A
* dubly-black의 오른쪽 형제가 black 이고 그 형제의 오른쪽 자녀가 red일 때
 >그 red를 doubly-black 위로 옮기고 옮긴 red로 extra black을 전달해서 red-and-black으로 만들면 black으로 바꾸고 해결

### case B
* dubly-black의 오른쪽 형제가 black 이고 그 형제의 왼쪽 자녀가 red이면서 그 형제의 오른쪽 자녀는 black일때
>doubly-black의 형제의 오른쪽 자녀가 red가 되게 만들면서 이후엔 caseA를 적용하여 해결

### case C
* doubly-black의 형제가 black이고, 그 형제의 자녀가 모두 black일때
>doubly-black과 그 형제의 black을 모아서 부모에게 전달해 부모가 extra-black을 해결하도록 위함임.

### case D
* doubly-black의 형제가 red일때
>doubly-black의 형제를 black으로 만든 후 case A,B,C중 하나로 해결

***
## RB 트리의 시간 복잡도
* 레드 블랙 트리는 균형 이진 탐색 트리(binary-search tree)로 탐색(Search), 삽입(Insert), 삭제(Delete) 모두 최악의 경우에도 O(logn)시간안에 가능하도록 해준다.

![image](https://velog.velcdn.com/images/youngcheon/post/696656fa-dffa-4bdd-934f-14f3deb8bf92/image.png)

출처 : https://velog.io/@youngcheon/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-Red-Black-Tree-%EC%82%AD%EC%A0%9C-%EA%B5%AC%ED%98%84


***

### 면접 예상 질문
>이진탐색 트리는 어떤 문제점이 있고, 이를 해결하기 위한 트리 중 한가지를 설명해보세요.


이진탐색트리 -> input이 이미 정렬되있다면 높이가 n -> 시간 복잡도 또한  O(n)







