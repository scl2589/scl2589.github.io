---
title:  "Greedy 문제 3탄"
excerpt: "Greedy 문제들을 풀어보았습니다 (3탄)."
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

- 오늘도 Greedy 문제들을 풀어보았습니다!

<br>

#### 문자열 뒤집기

##### 문제 설명

- 0과 1로 가진 문자열 S가 있습니다.
- S에서 연속된 하나 이상의 숫자를 잡고 모두 뒤집습니다. (1을 0으로, 0을 1로)

- 예시 

  - S = 000111일 때는?

    - trial 1
      - 전체를 뒤집으면: 111000
      - 4번째부터 6번째 문자까지 뒤집으면 111111이 되므로 두 번만에 모두 같은 숫자로 만들 수 있습니다.

    - trial 2
      - 하지만 4번째부터 6번째까지 문자를 뒤집으면 한 번에 000000이 되어서 1번 만에 모두 같은 숫자로 만들 수 있습니다.

- 문자열 S가 주어졌을 때 같은 숫자로 만들 수 있는 최소 횟수는?

<br>

##### 문제 접근 방식

- for loop 으로 돌아가면서 모든 수가 0일 때와, 모든 수가 1일 경우를 고려합니다.
- 그 각각의 경우를 따져 뒤집기 횟수를 계산합니다.

<br>

##### 문제 답안

- ```python
  S= [int(i) for i in list(input())]
  count0 = 0
  count1 = 0
  
  # 첫 번째 원소에 대해서 처리
  if S[0] == 0:
      count1 = 1
  else: 
      count0 = 1
  
  for i in range(1, len(S)):
      if S[i-1] != S[i]:
          # 다음 수가 0인 경우, 1로 바꿔준다.
          if S[i] == 0:
              count1 += 1
          # 다음 수가 1인 경우, 0으로 바꿔준다.
          else:
              count0 += 1
  print(min(count1, count0))
  ```

<br>

<br>

#### 만들 수 없는 금액

##### 문제 설명

- N개의 동전을 가지고 있을 때, 이를 이용하여 만들 수 없는 양의 정수 금액 중 최솟값을 구하는 프로그램을 작성하시오.
- 만약 N=5이고, 각 동전이 각각 3원, 2원, 1원, 1원, 9원짜리 동전이라 가정할 때, 만들 수 없는 양의 정수 금액 중 최솟값은 8원입니다.

<br>

##### 문제 입력 조건

- 첫째 줄: 동전의 개수 : N ( 1 <= N <= 1000)
- 둘째 줄 : 각 동전의 값을 나타내는 N개의 자연수가 주어짐

<br>

##### 문제 접근 방식

- 그리디 알고리즘으로의 접근 방식은 현재 상태에서 가장 best인 방식입니다.
- 동전들을 오름차순으로 정렬하여 가장 기본 단위부터 동전들의 총 금액까지 더해보면, 그 금액을 만들 수 있는지 혹은 없는지 확인할 수 있습니다.

<br>

##### 문제 답안

- ```python
  N = int(input())
  coins =list(map(int, input().split()))
  coins.sort()
  
  target = 1
  for x in coins:
      if target < x:
          break
      target += x
  
  print(target)
  ```

<br>

<br>

#### 볼링공 고르기

##### 문제 설명

- 주어진 볼링공 총 N 개 중에 1부터 M까지의 무게가 제공될때, 두 사람이 서로 다른 무게의 볼링공을 고르는 경우의 수를 구하는 프로그램을 작성하세요.

<br>

##### 문제 접근 방식

- 정렬 후, 무게마다 볼링공이 몇개가 있는지 계산합니다.
- A가 특정한 무게를 선택했을 때, B가 선택하는 경우의 수가 몇가지 있는지 확인하고 이를 모두 더하면 됩니다.

<br>

##### 문제 답안

- ```python
  N, M = map(int, input().split())
  arr = list(map(int, input().split()))
  
  array = [0] * 11
  
  for x in arr:
      # 각 무게에 해다하는 볼링공의 개수 카운트
      array[x] += 1
  
  result = 0
  
  # 1부터 m까지의 각 무게에 대하여 처리
  for i in range(1, m+1):
      n -= array[i] #무게가 i인 볼링공의 개수 (A가 선택할 수 있는 개수) 제외
      result += array[i] * n # B가 선택하는 경우의 수와 곱하기
  
  print(result)
  ```

  