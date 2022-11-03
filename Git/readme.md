# Git

## dev-interview-study contribution

### Git Repository에서 Fork하기
#### 1. https://github.com/93jpark/dev-interview-study 레포지토리 우측 상단 Fork 아이콘 클릭

![](/assets/images/instruction/git_instruction_1.png)

#### 2. Fork된 개인 레포지토리의 URL 복사

![](/assets/images/instruction/git_instruction_2.png)

#### 3. 다운로드 받을 경로로 이동하여 local repository로 clone

```
git clone [본인의 원격 repository 주소]

exmaple)
git clone https://github.com/93jpark/dev-interview-study
```

#### 4. local repository의 upstream이라는 브랜치에서 fork한 repository를 연결
```
git remote add upstream [fork한 repository 주소]

example)
git remote add upstream https://github.com/93jpark/dev-interview-study
```

<br>

---

<br>

#### 제대로 반영되었는지 확인하기
```
git remote -v
```
위의 명령어를 통해 local repository의 remote 상태를 확인할 수 있습니다.

![](/assets/images/instruction/git_instruction_3.png)
> origin : 현재 내가 작업중인 repository

본인_git_id/dev-interview-study.git 으로 보임.

> upstream : 내가 Fork해온 원본 repository
 
93jpark/dev-interview-study.git으로 보임.<sub>(내가 Fork해온 Repository 주소)</sub>


<br>

---

<br>

### 아래의 명령어들은 매 작업할때마다 반복 시행


<br>

#### 1. Local Repository에 Fork한 Repository의 업데이터 내역 불러오기
```
git fetch upstream
```




#### 2. 작업할 브랜치 생성
```
git checkout -b [브랜치_이름] [복사할_브랜치_이름]
example)
git checkout -b feature/week1준우 upstream/main
```

#### 3. 자유룝게 스터디🔥
👩‍💻🧑‍💻👨‍💻👩‍💻🧑‍💻👨‍💻👩‍💻🧑‍💻👨‍💻

<br>

#### 4. 정리 완료 시 작업한 브랜치에서 본인의 원격 repository로 push
```
git add .
git fetch upstream          ### push 하기 전 최신 변경사항 한번 더 적용
git merge upstream/main     ### push 하기 전 최신 변경사항을 현재 작업중인것에 적용하기
git commit -m "커밋 메시지"
git push origin feature/week1준우
```

#### 5. GitHub 원격 Repository로 이동하여 상단의 Comapre & pull request 버튼 클릭
> 본인의 fork한 repository에서 작업하면 됩니다.

![](/assets/images/instruction/git_instruction_4.png)


#### 6. Fork한 Repository에서 Pull Request 날리기

![](/assets/images/instruction/git_instruction_5.png)

#### 7. 단톡 등을 통해 PR날렸다고 알리기👏

