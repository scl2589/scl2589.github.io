---
title:  "병합정렬"
excerpt: "병합정렬(Merge Sort)에 대해 알아보았습니다."
date: 2020-12-26 02:12:51 
toc: true
toc_sticky: true
toc_label: "목차"
comments: true

categories:
  - datastructure

tags:
  - datastructure

sidebar:
    nav: "docs"

---



#### 개념

- 폰 노이만이 제안한 방법
- 분할 정복 알고리즘의 하나입니다.
  - 분할 정복 (divide and conquer) 이란?
    - 문제를 작은 2개의 문제로 분리하고, 각각을 해결한 다음, 그 결과를 모아서 원래의 문제를 해결하는 전략입니다.
    - 분할 정복 방법은 대개 순환 호출을 이용하여 구현합니다.
      - 순환 호출 = 재귀!
  - 병합정렬에서는 분할 정복이 어떻게 적용되나요?
    - divide: 입력 배열을 같은 크기의 2개의 부분 배열로 분할합니다.
    - conquer: 각 배열을 정렬합니다. 부분 배열의 크기가 충분히 작지 않으면 **순환 호출을** 이용하여 다시 분할 정복 방법을 적용합니다.
    - combine: 정렬된 부분 배열들을 하나의 배열에 합병합니다.
- 과정 설명
  - 리스트의 길이가 0 또는 1이면 이미 정렬된 것으로 봅니다.
  - 그렇지 않은 경우, 정렬되지 않은 리스트를 절반으로 잘라 비슷한 크기의 2개의 부분 리스트로 나눕니다.
  - 각 부분 리스트를 재귀적으로 합병 정렬을 이용해 정렬합니다.
  - 2개의 부분 리스트를 다시 하나의 정렬된 리스트로 합병합니다.
    - 합병할 때는 추가적인 리스트가 필요합니다!



#### 특징

- 장점
  - 안정적인 정렬 방법
    - 데이터의 분포에 영향을 덜 받습니다.
    - 즉, 입력 데이터가 무엇이든 정렬되는 시간은 동일합니다. ⇒ O(nlog2n)
  - 만약 레코드를 **연결 리스트 (Linked List)\**로 구성하면, 링크 인덱스만 변경되므로 데이터의 이동은 무시할 수 있을 정도로 작아집니다\**.**
  - 따라서 크기가 큰 레코드를 정렬한 경우에 연결 리스트를 사용하면 합병 정렬은 퀵 정렬을 포함한 다른 어떤 정렬 방법보다 효율적입니다.
- 단점
  - 만약 레코드를 배열 (Array)로 구성하면, 임시 배열이 필요합니다.
  - 레코드들의 크기가 큰 경우에는 이동 횟수가 많으므로 매우 큰 시간적 낭비를 초래합니다.



#### 시간복잡도

- O(nlogn)
- 최선, 최악도 모두 O(nlogn)이라는 점!



#### 예시

<img src="images/2020-12-25-mergesort/merge-sort-concepts.png" alt="img" style="zoom:50%;" />

<img src="images/2020-12-25-mergesort/merge-sort.png" alt="img" style="zoom:50%;" />

#### 구현

```python
def merge_sort(arr):
    if len(arr) < 2:
        return arr

    mid = len(arr) // 2
    low_arr = merge_sort(arr[:mid])
    high_arr = merge_sort(arr[mid:])

    merged_arr = []
    l = h = 0
    while l < len(low_arr) and h < len(high_arr):
        if low_arr[l] < high_arr[h]:
            merged_arr.append(low_arr[l])
            l += 1
        else:
            merged_arr.append(high_arr[h])
            h += 1
    merged_arr += low_arr[l:]
    merged_arr += high_arr[h:]
    return merged_arr
```



#### 참고

https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html

https://www.daleseo.com/sort-merge/