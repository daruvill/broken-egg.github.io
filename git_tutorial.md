# Git Hub Tutorial

## Contents (Table Of Content, TOC)

1. [Git 초기 설정](#git-초기-설정)
2. [Git 자주 쓰는 명령어](#git-자주-쓰는-명령어)
3. [Git 알아두면 좋은 명령어](#git-알아두면-좋은-명령어)
4. [기타 참고 사항](#기타-참고-사항)

---

## Git 초기 설정
#### 1/ 로컬 저장소 생성
먼저 하드 디스크에 작업 폴더(working tree)를 생성하고, 그곳에서 git bash(cli)를 실행하자.  
```bash
$git init
```
이후 위 명령어를 통해 현재 폴더에 git 로컬 저장소(.git)를 생성할 수 있다.

#### 2/ 유저 설정
```bash
$git config --global user.email 'dykim3277@gmail.com'

$git config --global user.name 'daruvill'

$git config --global core.editor #vscode가 아니라면 git을 재설치 해주는 것이 좋다.
```

#### 3/ 원격 저장소 설정
```bash
$git remote add origin https://github.com/daruvill/daruvill.github.io.git 
#origin : 원격 저장소(remote repository)의 이름. 우리가 사용하는 github이 바로 원격 저장소이다.
```
로컬 저장소에 원격 저장소의 주소를 등록한다.
```bash
$git push -u origin master #이후 push 이하의 옵션은 생략 가능
#upstream branch : 로컬 저장소와 연결된 원격 저장소  
#master : commit을 올리는 branch의 이름, 즉 로컬 저장소(local repository)의 메인이 되는 branch.  
#origin/master :  원격 저장소의 메인이 되는 branch.
```
이후 upstream branch를 원격 저장소의 master branch로 지정한다. (이해가 가지 않아도 그냥 따라하면 된다)

---

## Git 자주 쓰는 명령어
#### 1/ status
```bash
$git status
```
git 폴더에 변동 사항이 있는지 확인한다. 즉, 작업 폴더의 상태를 확인.  
작업 폴더, stage, HEAD 커밋의 3가지 저장 공간의 차이를 비교해서 보여준다.  
새로 파일을 생성할 경우, 작업 폴더에만 해당 파일이 존재한다.  
$add 실행 시 작업 폴더와 stage에 해당 파일이 존재한다.  
$commit 이후에 $status에서 출력되는 'working tree clean'은 위에서 언급한 3가지 저장 공간의 내용이 모두 동일함을 의미.

#### 2/ add
```bash
$git add README.md 
```
특정 파일을 stage에 추가한다.(=staging) 파일이 새로 생성된 경우 뿐만 아니라, 파일 내용이 수정된(modified) 경우에도 해주어야 한다.  

#### 3/ commit 
```bash
$git commit -m 'upload README.md'
#-m : 세이브 포인트 메모
```
현재 stage에 올라와 있는 파일들에 대해서 commit(세이브 포인트)을 작성한다.  
commit은 일반적으로 40자리 SHA1 해시 체크섬 값을 가지므로, 유일하게 식별 가능함.  
commit의 결과로서 commit 객체가 생기는데, 여기에는 부모 commit에 대한 참조와 실제 commit을 구성하는 파일 객체가 들어 있다.  
구체적으로 commit을 하면 stage의 객체로 tree가 만들어지는데, commit 객체에는 commit 메시지와 tree 객체가 포함된다.

#### 4/ push
```bash
$git push #위의 업스트림 설정으로 인해서 간단하게 사용 가능
```
로컬 저장소에 존재하는 커밋을 원격 저장소에 업로드. 즉, 현재 branch에서 새로 생성한 커밋들을 원격 저장소에 업로드.  

cf. 강제 push의 경우는 본인 혼자 사용하고 있는 branch에만 해야 하며, 일반적으로 사용을 추천하지 않는다.

#### 5/ log
```bash
$git log --all --oneline --graph
#--all : 모든 log 출력 (-n2와 같이 몇 라인만 출력 가능)
#--oneline : 한 줄로 요약하여 출력
#--graph : graph 형태로 표시하여 출력
#--decorate : ?
```
commit의 log를 확인한다.

---

## Git 알아두면 좋은 명령어

#### 0/ 파일 기본 개념
파일을 처음 생성한다면 untracked(추적 안 됨) 상태로 존재한다.  
이후 $add 실행 시 staged(스테이지 됨) 상태로 변한다.  
마지막으로 $commit 실행 시 unmodified(수정 없음) 상태로 변화한다.  
파일의 내용이 수정된다면 modified(수정 됨) 상태로 변하며, $add를 실행해 스테이지에 다시 올려주어야 한다.  
반면 unmodified 상태의 파일은 그대로 stage에 남아 있기 때문에, $commit 실행 시 함께 기록된다.

#### 1/ branch(가지)와 checkout

특정 시점에서 가지를 나누어 작업할 수 있는 기능. 새로운 가지로 커밋을 만들려면 반드시 branch를 먼저 만들어야 한다.  
새로운 커밋을 추가하면 master branch는 새로운 커밋을 가리키게 된다. 즉, branch는 특정한 커밋 객체 1개를 가리키는 일종의 포인터이다.  
branch를 넘나드는 것은 HEAD 포인터를 이용하는 방식인데, master branch의 포인터와 HEAD 포인터가 떨어진다면 detached HEAD가 된다.  
협업자는 커밋을 올릴 branch를 각각 만들고, 자신이 만든 branch로 이동하여 커밋을 올리고, 이후에 branch를 병합(merge)하면 된다.  

(Tip) 협업자끼리 branch 규칙을 미리 정해야 한다. 예를 들면 master branch에는 직접 커밋을 올리지 않는다던지, master branch를 기준으로  
새로운 branch를 만들고 작업을 한다던지, 특정한 이름 형식으로 만든다던지, 작업 종료 후 해당 branch를 master branch에 병합한다던지.  
branch는 주로 새로운 기능 추가, 버그 수정, 병합과 리베이스 테스트, 이전 코드 개선, 특정 커밋으로 돌아가고 싶을 때 사용한다.  

```bash
$git branch mybranch1
```
(HEAD 포인터가 가리키는 곳에서) branch를 새롭게 생성한다.

```bash
$git checkout mybranch1
```
특정한 branch로 이동한다. log를 통해 HEAD 포인터가 변경되었다면 성공적으로 이동한 것이다.  
구체적으로는 해당 branch로 HEAD 포인터를 이동시키고, stage와 작업 폴더를 HEAD가 가리키는 커밋과 동일한 내용으로 변경한다.

```bash
$git checkout 5813bb5
```
branch 이름 대신 커밋 ID값 앞 7자리 또는 전체를 사용하여 이동하는 것도 가능하다.  
하지만 이는 HEAD 포인터가 branch와 분리될 수 있으므로 추천하지 않는다.

```bash
$git checkout -
```
이전 브랜치(커밋)로 이동한다.

```bash
$git branch -d mybranch1
```
특정한 local branch를 제거한다. HEAD가 가리키는 branch나 병합이 되지 않은 branch는 삭제 불가.

```bash
$git push origin -d mybranch1
```
특정한 remote branch를 제거한다. 삭제할 일이 없는 편이 좋다.

```bash
$git branch -v #로컬 저장소의 branch 목록을 출력
#-r : 원격 저장소에 있는 브랜치 목록을 출력
```

```bash
$git checkout -b mybranch1 master
```
특정 branch(master branch)에서 새로운 branch(mybranch1)를 생성하고 해당 branch로 이동.  

#### 2/ 기타 
```bash
$git remote -v #원격 저장소 목록 출력
```

```bash
$git clone https://github.com/daruvill/daruvill.github.io.git mynewfolder1 #특정 저장소의 코드와 버전 전체를 다운로드
```

```bash
$git reset README.md #stage 영역에 있는 파일을 stage에서 내림(=unstaging, add의 반대 기능)
#즉, 파일은 add 명령을 실행하기 이전인 untracked(추적 안 됨)의 상태로 돌아간다.
```

```bash
$git rm README.md #reset과 마찬가지로 unstaging이지만, 폴더에 존재하는 실제 파일도 함께 삭제하므로 유의.
```

#### 3/ merge(병합)

```bash
$git merge mybranch1 #현재 HEAD가 가리키는 branch가 master라는 전제 하에, mybranch1을 master에 병합
#즉, master branch의 내용 갱신이라고 보면 된다.
```
지정한 branch의 커밋을 현재 branch 및 작업 폴더에 반영. 일종의 두 버전의 합집합을 구하는 것.  
새로운 상태의 커밋이라면 병합 커밋이 생성된다. 병합한 결과물이 어느 한 쪽과 동일하다면 fast-forward(빨리 감기) 병합.  
그 밖에는 충돌 상태(conflict)도 존재.

#### 4/ pull

```bash
$git pull origin master
```
원격 저장소에 새로운 커밋이 존재한다면 이를 로컬 저장소로 내려 받는다. 즉, 원격 저장소의 변경 사항을 작업 폴더에 반영.  
명령어로 보자면 pull = fetch + merge라고 볼 수 있다.

#### 5/ reset

```bash
$git reset --hard HEAD~2
#--hard : 완전한 reset
#--mixed : 기록이 남는 reset
#HEAD~2 : 2번째 위쪽 부모. 즉, 조부모 커밋.
```
현재 branch를 지정한 커밋으로 옮긴다. 작업 폴더의 내용도 함께 변경된다. 즉, 현재 branch를 특정 커밋으로 되돌릴 때 사용.  
또는 특정 커밋까지 현재 branch를 초기화.

#### 6/ revert

```bash

```
커밋 되돌리기. ctrl + z?  
최신 커밋부터 취소를 하는 것이 좋다.

#### 7/ fetch

```bash
```
원격 저장소의 branch와 커밋을 로컬 저장소와 동기화한다.

## 기타 참고 사항

#### 1/ branch 폴더
```bash
$ls .git/refs/heads/ 
```
생성된 branch들이 위치한 폴더의 파일 리스트를 확인한다. 
해당 폴더의 branch 이름에 해당하는 파일을 제거하면 해당 branch가 제거된다.  
즉, *$git branch -d mybranch1 == $rm .git/refs/heads/mybranch1*

#### 2/ HEAD 포인터 및 파일
```bash
$cat .git/HEAD
```
해당 파일을 통해 HEAD 포인터가 가리키고 있는 branch를 알 수 있다.  
HEAD 포인터는 현재 작업중인 branch를 의미하며, branch는 커밋을 가리키므로 HEAD 포인터 역시 커밋을 가리킨다.  
즉, HEAD 포인터는 현재 작업 중인 branch의 최근 커밋을 가리킨다.

#### 3/ Git 객체
```bash
$ls -a .git/objects/ #Git 객체들이 위치한 폴더

$ls -a .git/objects/ff #폴더명+파일명을 합치면 파일의 체크섬 값과 일치

$git show ff5bda #파일의 체크섬 값을 통해서 해당 Git 객체의 내용을 볼 수 있음
```
생성된 Git 객체들이 위치한 폴더의 파일 리스트를 확인한다. 커밋 역시 객체이므로, 위 폴더에 저장된다.  
스테이지에 올라간 파일 객체는 blob(binary large object)이 된다.  
blob은 제목이나 생성 날짜와는 관계 없이 내용이 같을 경우 같은 체크섬을 가진다.  
따라서 같은 내용의 파일은 하나의 blob으로서 관리된다.

#### 4/ Stage
```bash
$git hash-object README.md #특정 파일의 체크섬 값을 확인

$git add README.md #stage에 특정 파일 추가

$ls -a .git/index #index 파일 = Git Stage

$git ls-files --stage #stage 파일의 내용 확인
```
같은 내용의 파일이라면 언제나 똑같은 hash checksum 값을 가진다.

#### 5/ 임시 branch 생성
```bash
$git branch mytestbranch1 mybranch1 #특정 branch(mybranch1)에서 임시 branch(mytestbranch1) 생성
```
임시 branch를 생성하여 코드를 테스트 한 후 이를 제거하면 아무런 문제가 없다.

#### 6/ tag 부착
```bash
$git tag -a -m 'first tag' v0.1
#tag -a -m <message> <tag name> <branch or checksum>
#<branch> 생략 시 HEAD 포인터에 tag를 생성

$git push origin v0.1 #원격 저장소에 tag 업로드
```
특정 커밋에 포스트잇을 붙이는 느낌으로 이해하면 된다. branch와 마찬가지로 일종의 포인터.  
사용자들이 크게 느낄 변화를 적용했을 때는 메이저 버전을 올리고, 작은 변화가 생겼을 때는 마이너 버전을 올린다.  

#### 7/ pull request
협력자에게 branch merge를 요청하는 메시지를 보내는 것.

#### 8/ fork
다른 유저의 원본 저장소를 내 계정의 원격 저장소로 복사하는 기능.  
5명 이내의 적은 개발자가 협업을 한다면 모두 협업자로 등록하는 것이 좋지만, 50명 이상이 작업을 한다면 fork가 필요.  

#### 9/ README.md
저장소에 대한 설명, 설치 방법, 기여한 사람 등을 작성하는 파일. contribution guideline이 적혀있는 경우도 있으니 확인 필요.  
MIT License의 경우, 해당 소스를 재가공해서 재배포해도 된다는 것을 의미한다.  

#### 10/ branch 이름
1) feat : 각 개발자가 개발 중인 branch. 직접 커밋을 올림.  
2) master : feat branch에서 개발 완료된 코드가 합쳐진 branch. 일종의 베타 버전이며, 병합을 통해서만 코드를 업데이트. 직접 커밋을 올리지 않음.  
3) latest : 실제 출시할 코드를 올리는 branch. master branch에서 굵직한 개발이 끝나면 출시 시점에 latest branch로 코드를 병합.
4) hotFix, bugFix : 버그 수정을 목적으로 만들어진 branch.

#### 11/ cherry-pick(선별하다)
내가 따길 원하는 특정 커밋을 선택하여 이를 반영. 즉, 다른 branch의 커밋 하나만을 나의 branch에 반영할 수 있음.

#### 12/ stash (넣어두다)
커밋으로 만들기는 애매하지만, 변경 사항을 잠깐 서랍 속에 넣어뒀다가 다시 꺼내쓰고 싶을 때 사용. tracked 상태인 파일만 들어갈 수 있음.  

#### 13/ bash
bash 창에서 붙여넣기는 Ctrl+v가 아닌 Shift + insert이다.

#### 14/ commit message
좋은 커밋 메시지란 제목과 본문을 빈 줄로 구분. 제목은 50자 이내, 본문은 72자 단위로 줄 바꿈. what과 why를 위주로 설명.

#### 15/ rebase
```bash
$git rebase mybranch1
```
현재 branch에만 있는 새로운 커밋을 특정 branch 위로 재배치. 빨리감기 병합이 가능한 경우 이를 실행함.  
HEAD 포인터와 특정 branch의 공통 조상을 찾고, 공통 조상 이후에 생성한 커밋들을 특정 branch 뒤로 재배치하는 원리.  
3-way merge와는 달리 rebase를 이용하면 history graph는 깔끔해지지만 conflict가 여러 번 발생할 수 있으므로 주의.  
원격 저장소에 push한 branch는 rebase 하지 않는 것이 원칙. 따라서 rebase는 로컬 저장소의 branch에만 적용하는 것을 권장.  
그렇지 않으면 사본 커밋들이 무수히 생겨나고 history가 꼬일 수 있음.

#### 16/ 여러 대의 pc에서 작업을 할 경우
여러 대의 PC에서 한 branch에 작업을 하는 경우, 한 PC에서는 커밋을 생성하고 push를 했는데, 다른 PC에서는 pull을 하지 않고 커밋을 하면 문제가 발생.  
뒤늦게 pull을 시도하면 자동으로 3-way merge가 발생하므로 그래프가 복잡해진다. 이러한 경우 $reset --hard로 병합 커밋을 되돌리고, rebase를 사용하면 됨.  

**출처 : << 팀 개발을 위한 Git GitHub 시작하기 / 정호영, 진유림 >>**