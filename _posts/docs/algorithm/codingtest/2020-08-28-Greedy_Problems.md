---
title:  "Greedy 문제"
excerpt: "2019 국가 교육기관 코딩 테스트 문제인 '큰 수의 법칙'을 풀어보았습니다."
date: 2020-08-28 01:15:00 
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

- 나동빈님의 '이것이 취업을 위한 코딩 테스트다' 책을 보며 풀어본 그리디 문제입니다.



#### 문제 설명

- **큰 수의 법칙**
  - 배열이 다양한 수로 이루어졌을 때, 주어진 수들을 M번 더하여 가장 큰 수를 만드는 법칙입니다.
  - 그러나, 인덱스에 해당하는 수가 연속해서 K번을 초과하여 더해질 수는 없습니다.
- 예시
  - 배열: [7, 6, 7, 6, 5] 이 존재하고, 
  - K가 3, M이 6이라면, 
  - 7 + 7 + 7 + 6 + 7 + 7 = 41이 됩니다.
- 입력 예시
  - N (배열의 크기), M (숫자가 더해지는 횟수), K (연속해서 더할 수 있는 횟수)
  - 배열



#### 문제 접근 

- 위 방식은 전형적인 알고리즘 문제로 머릿속에 떠오르는 아이디어를 이용합니다.
- 이를 위해서는 가장 큰 숫자와 두 번째로 큰 숫자를 찾습니다.
- 이를 위해 K 번 가장 큰 숫자를 더하고, 그 이후 1번만 두 번째로 큰 숫자를 더하고 이가 반복되는 형태가 됩니다.



#### 문제 답안

- ```python
  N, M, K = map(int, input().split())
  
  arr = list(map(int, input().split()))
  
  # 정렬하기
  arr.sort()
  
  # 가장 큰 수
  largest = arr[-1]
  
  # 두 번째로 큰 수
  second = arr[-2]
  
  result = 0
  # 가장 큰 수가 더해지는 횟수 계산 
  result += M // K * K * largest
  # 두번째로 큰 수 더하기 
  result += M % K * second
  
  print(result)
  ```

  