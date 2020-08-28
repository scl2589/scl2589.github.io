---
title:  "Greedy 문제 2탄"
excerpt: "Greedy 문제들을 풀어보았습니다 (2탄)."
date: 2020-08-29 00:30:00 
toc: true
toc_sticky: true
toc_label: "목차"
comments: true

categories:
  - codingtest

tags:
  - greedy
  - codingtest

sidebar:
​    nav: "docs"
---



### Intro

- 오늘은 그리디 문제인 '모험가 길드' 문제를 풀어보았습니다.

<br>

#### 모험가 길드

##### 문제 설명

N명의 모험가를 대상으로 '공포도'를 측정합니다.

공포도가 X인 모험가는 반드시 X명 이상으로 구성한 모험가 그룹에 참여해야 여행을 떠날 수 있습니다.

그렇다면 여행을 떠날 수 있는 그룹 수의 최댓값은 무엇일까요?





##### 문제 접근 

이 문제를 풀기 위해서는 공포도에 따라 X명으로 구성된 그룹을 만들어야 하므로, 공포도가 낮은 사람을 먼저 찾아야 합니다.

공포도가 낮은 사람으로 구성될 수록 더 적은 인원으로 그룹을 형성할 수 있으므로, 오름차순 정렬을 이용합니다.



##### 입력 예시

- 5 (모험가 수 N)
- 2 3 1 2 2 (각 모험가의 공포도 값)



##### 문제 답안

- ```python
  N = int(input())
  arr = list(map(int, input().split()))
  
  arr.sort()
  total = 0
  count = 0
  
  for i in arr:
      total += 1
      if total >= i:
          count +=1
          total = 0
  
  print(count)
  ```

<br>

#### 곱하기 혹은 더하기

##### 문제 설명

각 자리가 숫자로만 이루어진 문자열 S가 주어집니다.

왼쪽부터 오른쪽으로 하나씩 모든 숫자를 확인하며 '+' 혹은 'x' 연산자를 넣어 결과적으로 가장 큰 숫자를 만들 수 있는 프로그램을 작성하세요.

단, 연산은 연산자의 우선순위와 상관없이 왼쪽부터 계산합니다.



##### 문제 접근

이 문제를 풀기 위해서는 한 가지만 생각하면 된다.

만약 연산하려는 두 수 중에서 하나라도 숫자가 '0'이거나 '1'이라면 더하기를 해야 값이 더 커질 수 있고, 그 이외이면 곱하면 된다.



##### 문제 답안

- ```python
  S= [int(i) for i in list(input())]
  max = 0
  first = S[0]
  for i in range(1, len(S)):
      num = S[i]
      if num <= 1 or first <= 1:
          first += num
      else:
          first *= num 
  print(first) 
  
  ```
  
  
