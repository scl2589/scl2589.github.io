---
title:  "커밋 날짜를 수정하는 방법"
excerpt: "Commit 날짜 수정하는 방법을 알아보았습니다."
date: 2020-06-16 12:00:00 
toc: true
toc_sticky: true
toc_label: "목차"
comments: true

categories:
  - git

tags:
  - git
  - commit

sidebar:
​    nav: "docs"

---



#### 커밋 날짜 수정이 필요한 이유

---

- 코딩이나 문서 작업을 진행했지만, 12시가 넘어가 commit을 해버린 경우, github나 gitlab 등에서는 commit한 날짜와 시간으로  잔디 심기가 진행됩니다.

- 이렇게 특정일을 놓쳤을 때 유용하게 사용할 수 있는 방법입니다.

<br>

<br>

#### 가장 최근 commit일 경우

##### 가장 최근 Commit 날짜를 현재 날짜로 설정 

- ```bash
  $ git commit --amend --no-edit --date "$(date)"
  ```

##### 가장 최근 Commit 날짜를 임의의 날짜로 설정

- ```bash
  $ git commit --amend --no-edit --date "Mon 20 Aug 2018 20:19:19 KST"
  ```

- `""`사이에 설정하고 싶은 날짜와 시간을 기입하면 됩니다.

<br>

<br>

#### 과거 commit일 경우

- 만약 날짜를 바꿀 commit이 가장 최근 commit이 아니라면 다음과 같이 설정합니다.

##### 해시 값 찾기

- 먼저 git log를 통해 **commit 해시 값**을 찾습니다.

  - ```bash
    $ git log
    ```

- 위 명령어를 치면 다음과 같은 화면이 나옵니다.

  - ```bash
    commit 964c654f1af90ca4e2e4608f69268d405436c196 (HEAD -> master, origin/master)
    Author: 신채린 <chaelinshin96@gmail.com>
    Date:   Mon Sep 7 12:00:30 2020 +0900
    
        Add 20200907 Baekjoon 13458_시험감독
    
    commit 97d77a4c5efbf49404cb6cf55e8e4d1724fb4d5f
    Author: 신채린 <chaelinshin96@gmail.com>
    Date:   Sat Sep 5 02:42:23 2020 +0900
    
        Add 20200905 JavaScript History
    
    commit ce460413b426ac2008e9a1575c2fbff37710173e
    Author: 신채린 <chaelinshin96@gmail.com>
    Date:   Sat Sep 5 01:12:26 2020 +0900
    	
    	 Add 20200826 JavaScript For Loop and Sort
    ```

- commit 해시 값이란 <u>commit 우측에 써져있는 값</u>을 말합니다.
- 기본적으로 rebase 명령어를 이용할 때 는 **변경하고자 하는 commit의 *<u>이전 commit</u>*을 기준**으로 기입해줍니다.

<br>

##### edit 적용하기

- 이후 변경하고자 하는 commit을 선택 내용을 <u>키보드 `i`를 눌러</u> **edit으로 바꿔 적용**하면 됩니다.

<br>

##### 날짜 변경하기

- 그 이후 다음 명령어로 커밋 내역의 날짜를 변경합니다.

  - ```bash
    $ GIT_COMMITTER_DATE="{원하는 날짜}" git commit --amend --no-edit --date "{원하는 날짜}"
    ```

  - 예시: `GIT_COMMITTER_DATE="Jun 16 10:00:00 2020 KST" git commit --amend --no-edit --date "Jun 16 10:00:00 2020 KST"`

<br>

##### 변경 내용 적용하기

- 날짜를 변경한 후, 이 변경 내역을 적용하고 싶다면 다음 코드를 작성합니다.

  - ```bash
    $ git rebase --continue
    ```

<br>

##### 푸시하기

- 변경 내용을 적용했다면, 깃허브에 푸시합니다.

- ```bash
  $ git push -f origin master
  ```

  