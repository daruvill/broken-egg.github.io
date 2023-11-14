# Git Hub Tutorial

## Git 초기 설정
#### 1/ 로컬 저장소 생성
먼저 하드 디스크에 작업 폴더(working tree)를 생성하고, 그곳에서 git bash(cli)를 실행하자.  
```bash
$git init
```
이후 위 명령어를 통해 현재 폴더에 git 로컬 저장소(.git)를 생성할 수 있다.

#### 2/ 초기 유저 설정
```bash
$git config --global user.email 'dykim3277@gmail.com'

$git config --global user.name 'daruvill'
```

#### 3/ 원격 저장소 설정
```bash
$git remote add origin https://github.com/daruvill/daruvill.github.io.git 
#origin : 원격 저장소(remote repository)의 이름
```
로컬 저장소에 원격 저장소의 주소를 등록한다.
```bash
$git push -u origin master #이후 push 이하의 옵션은 생략 가능
#upstream branch : 로컬 저장소와 연결된 원격 저장소  
#master : commit을 올리는 branch의 이름, 즉 로컬 저장소(local repository)의 메인이 되는 branch.  
#origin/master :  원격 저장소의 메인이 되는 branch.
```
upstream branch를 원격 저장소의 master branch로 지정한다.

## Git 자주 쓰는 명령어
#### 1/ status
```bash
$git status
```
git 폴더에 변동 사항이 있는지 확인한다. 즉, 작업 폴더의 상태를 확인.

#### 2/ add
```bash
$git add README.md 
#README.md : 저장소에 대한 설명, 설치 방법, 기여한 사람 등을 작성.
```
특정 파일을 stage에 추가한다.(=staging) 파일이 새로 생성된 경우 뿐만 아니라, 파일 내용이 수정된 경우에도 staging을 다시 해주어야 한다.  

#### 3/ commit 
```bash
$git commit -m 'upload README.md'
#-m : 세이브 포인트 메모
```
현재 stage에 대해서 commit(세이브 포인트)을 작성한다.

#### 4/ push
```bash
$git push #위의 업스트림 설정으로 인해서 간단하게 사용 가능
```
커밋을 원격 저장소에 업로드한다.

#### 5/ log
```bash
$git log --all --oneline --graph
#--all : 모든 log 출력 (-n2와 같이 몇 라인만 출력 가능)
#--oneline : 한 줄로 요약하여 출력
#--graph : graph 형태로 표시하여 출력
```
commit의 log를 확인한다.

## Git 알아두면 좋은 명령어

#### 1/ branch 개념
```bash
$git branch mybranch1 #branch 생성

$git checkout mybranch1 #특정 branch로 이동. log를 통해 HEAD 포인터가 변경된 것을 알 수 있음.

$git checkout 5813bb5 #branch 이름 대신 커밋 ID값 앞 7자리 또는 전체를 사용 가능

$git checkout - #이전 브랜치(커밋)로 이동

#요컨대, 특정 branch를 생성하고 그곳에 커밋을 하는 것 자체가 협업의 시작이다.
```

```bash
$git remote -v #원격 저장소 목록 출력
```

```bash
$git clone https://github.com/daruvill/daruvill.github.io.git #특정 저장소의 코드와 버전 전체를 다운로드
```

```bash
$git reset README.md #stage 영역에 있는 파일을 stage에서 내림(=unstaging, add의 반대 기능)
#즉, 파일은 add 명령을 실행하기 이전인 untracked(추적 안 됨)의 상태로 돌아간다.
```

```bash
$git rm README.md #reset과 마찬가지로 unstaging이지만, 폴더에 존재하는 실제 파일도 함께 삭제하므로 유의.
```

#### 2/ merge(병합) 개념

```bash
$git merge mybranch1 #현재 HEAD가 가리키는 branch가 master라는 전제 하에, mybranch1을 master에 병합
#즉, master branch의 내용 갱신이라고 보면 된다.
```

## Git 실전 사용 사례 1

**출처 : <팀 개발을 위한 Git GitHub 시작하기 / 정호영, 진유림>**