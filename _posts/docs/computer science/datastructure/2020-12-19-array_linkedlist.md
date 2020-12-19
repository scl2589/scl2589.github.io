---
title:  "Array vs Linked List"
excerpt: "Array와 Linked List의 차이를 알아보았습니다."
date: 2020-12-19 13:33:51 
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



### 간단 정리

### 배열

- 특징
  - 논리적 저장순서와 물리적 저장 순서가 일치합니다.
  - 인덱스로 해당 원소에 접근이 가능합니다. 그래서 데이터 검색에 유리합니다.
    - 인덱스만 알고 있다면 O(1) 가능
  - Random Access가 가능합니다.
  - 배열의 원소를 삭제할 경우 삭제한 원소보다 큰 인덱스를 가진 원소들을 옮겨줘야(Shift) 하기 때문에 시간 복잡도 O(n)이 걸립니다.
  - 삽입의 경우, 새로운 원소를 추가하고 모든 원소들의 인덱스를 1씩 Shift 해줘야 하므로 시간 복잡도 O(n)이 걸린다.
  - 제한적인 크기를 갖는다.

<br>

### 링크드리스트

![img](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/dd9a82d4-3782-4aaa-b62e-689c3f44d781/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20201222%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20201222T093147Z&X-Amz-Expires=86400&X-Amz-Signature=817ba2e70e4681659948e22298304bbab3ff588921e2e7c903b50d1ca0a20487&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

- 특징

  - 자료의 주소 값으로 노드를 이용해 서로 연결되어 있는 구조를 갖습니다
  - 배열과 다르게 element와 element 간의 연결(link)을 이용해서 리스트를 구현한 것
  - 트리의 근간이 되는 자료구조입니다.

- 장점

  - **삽입과 삭제가 O(1)**에 이루어집니다.
    - 삽입과 삭제를 할 때마다 동적으로 링크드 리스트의 크기가 결정되므로 전통적인 배열(Array)에 비해 처음부터 큰 공간을 할당할 필요가 없어집니다.
  - **메모리 관리가 용이합니다**. (사실상 이게 가장 큰 이유.)

- 단점

  - Random Access, 즉 **배열처럼 index를 통해 탐색이 불가능**합니다.
  - **탐색이 O(N)**이 걸립니다. (Head부터 Tail까지 모두 탐색 시)
  - 삽입과 삭제
    - 사실상 삽입과 삭제가 왼쪽에서(Head에서) 이루어지지 않을 경우, 결국 탐색을 먼저 해야 하기 때문에 삽입과 삭제 모두 적게는 O(k)부터 최악의 경우 O(N)까지 걸릴 가능성이 있습니다.
  - 파이썬에서 링크드 리스트는 의미가 크게 없는 게, 그냥 리스트 쓰면 된다. C++의 STL vector보다도 훨씬 쓰기 간편하며, 어떠한 타입의 데이터도(심지어 튜플이나 리스트마저) 넣을 수 있고 동적으로 메모리 관리가 되기 때문에, 링크드 리스트의 의미가 크게 퇴색됩니다.

- linked list 코드

  - ```python
    # Node 클래스 정의
    class Node:
        def __init__(self, data):
            self.data = data
            self.next = None
    
    
    # LinkedList 클래스 (자료구조) 정의
    class LinkedList:
    
        # 초기화 메소드
        def __init__(self):
            dummy = Node("dummy")
            self.head = dummy
            self.tail = dummy
    
            self.current = None
            self.before = None
    
            self.num_of_data = 0
    
        # append 메소드 (insert - 맨 뒤에 노드 추가, tail과 node의 next, 데이터 개수 변경)
        def append(self, data):
            new_node = Node(data)
            self.tail.next = new_node
            self.tail = new_node
    
            self.num_of_data += 1
    
        # delete 메소드 (delete - current 노드 삭제, 인접 노드의 current, next 변경, 데이터 개수 변경)
        def delete(self):
            pop_data = self.current.data
    
            if self.current is self.tail:
                self.tail = self.before
    
            self.before.next = self.current.next
            self.current = self.before # 중요 : current가 next가 아닌 before로 변경된다.
            #
    
            self.num_of_data -= 1
    
            return pop_data
    
        # first 메소드 (search1 - 맨 앞의 노드 검색, before, current 변경)
        def first(self):
            if self.num_of_data == 0: # 데이터가 없는 경우 첫번째 노드도 없기 때문에 None 리턴
                return None
    
            self.before = self.head
            self.current = self.head.next
    
            return self.current.data
    
        # next 메소드 (search2 - current 노드의 다음 노드 검색, 이전에 first 메소드가 한번은 실행되어야 함)
        def next(self):
            if self.current.next == None:
                return None
    
            self.before = self.current
            self.current = self.current.next
    
            return self.current.data
    
        def size(self):
            return self.num_of_data
    ```

<br>

#### 차이

##### 연산시간

- 데이터 접근 속도
  - Array > Linked List
  - Array
    - 인덱스를 사용해 빠르게 원소에 접근할 수 있습니다. 따라서 **Random Access**를 지원합니다.
    - `시간 복잡도 O(1)`로 빠르게 찾을 수 있습니다.
  - Linked List
    - Sequential Access (순차 접근 방식)을 사용합니다.
    - 특정 원소에 접근하기 위해서는 처음부터 원소에 도달할 때까지 순차적으로 검색하면서 찾습니다.
    - `시간 복잡도 O(N)`
- 데이터 삽입 속도
  - 보통 Linked List > Array
  - Array
    - 데이터를 중간이나 맨 앞에 삽입할 경우, 그 이후의 데이터를 한 칸씩 미뤄야 하는 추가 과정과 시간이 소요됩니다.
    - 데이터가 많을 경우 비효율적입니다.
    - 그렇기 때문에 LinkedList가 필요하게 되었습니다.
  - Linked List
    - 어느 곳에 삽입하던지 O(n)의 시간복잡도를 갖습니다.
      - 삽입할 위치를 찾고(O(n)) 삽입 연산을 진행하기 때문에 O(N)의 시간 복잡도를 갖습니다.
    - 만약, 중간 삽입이 없다면 즉 맨 앞과 맨 뒤에만 삽입한다면 `시간 복잡도 : O(1)`
- 데이터 삭제 속도
  - 이 부분도 경우에 따라 다릅니다. (보통 Linked List > Array)
  - Array
    - 그 위치의 데이터를 삭제 후, 전체적으로 Shift 해줘야 합니다.
    - `시간 복잡도 O(N)`
  - LinkedList
    - 삭제할 원소를 찾기 위해서 O(N)의 시간 복잡도를 갖고 삭제를 합니다.
    - `시간 복잡도 O(N)`
    - 하지만 Array 보다 빠르게 삭제 연산을 수행합니다.
    - 만약, 중간 삭제가 없고 맨 앞과 뒤에서만 삭제한다면 `시간 복잡 O(1)`

<br>

##### **저장 방식**

- Array
  - element들은 **인접한** **memory** **위치**에 저장 되거나 memory에 연이어 저장됩니다.
- LinkedList
  - 새로운 element들은 memory 어딘가에 저장되어 되어집니다.
  - 새로운 element에 할당된 memory 위치 주소는 linked list의 **이전 node**에 저장되어집니다.

<br>

##### **Memory Allocation (메모리 할당)**

- Array
  - Array가 선언되자 마자 memory는 compile time에 할당되어집니다.
  - 이것을 **Static Memory Allocation (정적 메모리 할당)**이라고 불립니다.
  - Array는 **Stack** 영역에 memory 할당이 이루어집니다.
- LinkedList
  - 메모리는 새로운 node가 추가될 때 runtime에 할당되어집니다.
  - 이것을 **Dynamic Memory Allocation (동적 메모리 할당)**이라고 불립니다.
  - LinkedList는 **Heap** 영역에 memory 할당이 이루어집니다.
- static memory allocation vs dynamic memory allocation
  - static memory allocation
    - **고정된 영역**에만 memory를 할당합니다.
  - dynamic memory allocation
    - 프로세스가 돌아가는 **runtime 내에 영역의 크기를 알려줌**으로써 영역을 확보합니다.
- Stack vs Heap
  - stack
    - 메모리의 스택(stack) 영역은 **함수의 호출과 관계되는 지역 변수와 매개변수가 저장되는 영역**입니다.
    - 스택 영역은 함수의 호출과 함께 할당되며, 함수의 호출이 완료되면 소멸합니다.
    - 이렇게 스택 영역에 저장되는 함수의 호출 정보를 스택 프레임(stack frame)이라고 합니다.
    - 스택 영역은 푸시(push) 동작으로 데이터를 저장하고, 팝(pop) 동작으로 데이터를 인출합니다.
    - 이러한 스택은 **후입선출(LIFO, Last-In First-Out) 방식**에 따라 동작하므로, 가장 늦게 저장된 데이터가 가장 먼저 인출됩니다.
    - 스택 영역은 메모리의 높은 주소에서 낮은 주소의 방향으로 할당됩니다.
  - heap
    - 변수는 전역적으로 접근이 가능합니다.
    - 메모리의 힙(heap) 영역은 사용자가 직접 관리할 수 있는 ‘그리고 해야만 하는’ 메모리 영역입니다.
    - 힙 영역은 사용자에 의해 메모리 공간이 동적으로 할당되고 해제됩니다.
    - 힙 영역은 메모리의 낮은 주소에서 높은 주소의 방향으로 할당됩니다.

<br>

##### **Size**

- array
  - size는 반드시 array 선언 시점에 지정되어있어야 합니다.
- LinkedList
  - size는 다양할 수 있습니다.
  - node들이 추가될 때 runtime 시점에서 LinkedList size는 커질 수 있기 때문입니다.

<br>

##### **종류**

- Array
  - **single dimensional**
  - **two dimensional**
  - **multidimensional**
- Linked List
  - **Linear(Singly) linked list**
  - **Doubly linked list**
  - **Circular linked list**

<br>

### 번외 1) 배열(Array)과 리스트(ArrayList)의 차이는?

- 정리
  - 배열
    - 데이터의 크기가 정해져 있고, 추가적인 삽입 삭제가 일어 나지 않으며 검색을 필요로 할 때 유리.
  - 리스트
    - 데이터의 크기가 정해져 있지 않고, 데이터에 순서가 있으며, 삽입 삭제가 많이 일어나고, 검색이 적은 경우 유리.
- 배열
  - 특징
    - 같은 자료형을 가진 변수를 하나로 나타낸 것.
    - 연속된 메모리 공간으로 이루어져있는 것.
    - 정적 표현.
    - 인덱스를 이용하여 표현.
    - 지역성을 가지고 있다.
  - 장단점
    - 배열의 장점
      - 인덱스를 통한 검색이 용이함.
      - 연속적이므로 메모리 관리가 편하다.
    - 배열의 단점
      - 한 데이터를 삭제하더라도 배열은 연속해야 하므로 공간이 남는다. 즉, 메모리 낭비
      - 정적이므로 배열의 크기를 컴파일 이전에 정해주어야 한다.
      - 컴파일 이후 배열의 크기를 변동 할 수 없다.
  - 제공언어
    - Java
    - Javascript (자바스크립트는 배열에 리스트 기능 포함)
    - C
- 리스트
  - 특징
    - **순서가 있는** 데이터의 집합.
    - 불연속적으로 메모리 공간을 차지.
    - 동적 표현
    - 인덱스가 없음.
    - **포인터**를 통한 접근
  - 리스트의 장단점
    - 리스트의 장점
      - 포인터를 통하여 다음 데이터의 위치를 가르켜고 있어 삽입 삭제의 용이.
      - 동적이므로 크기가 정해져 있지 않다.
      - 메모리의 재사용 편리
      - 불연속적이므로 메모리 관리의 편리
    - 리스트의 단점
      - 검색 성능이 좋지 않다.
      - 포인터를 통해 다음 데이터를 가르키므로 추가적인 메모리 공간 발생.
  - 제공언어
    - Python
    - Java

<br>

### 번외 2) Doubly Linked List

![img](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7b86fda1-4449-47ee-bfe6-12b9a1f6d9c8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20201222%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20201222T093219Z&X-Amz-Expires=86400&X-Amz-Signature=e0f5cce245e55a7602b662976c5ee0c8ea667b1d4b7a168bf8cde92a70dde872&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

- 시간복잡도

  ![img](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ace7a7c6-9921-4530-95c9-4ed2d6c78277/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20201222%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20201222T093236Z&X-Amz-Expires=86400&X-Amz-Signature=3aee0ee938da800240ded6f7abd51262a21ce3a97712cb63f260477c76e30a2f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

- 장점

  - 싱글 링크드 리스트와 모든 장점을 공유한다.
    - 삽입과 삭제가 O(1)에 이루어진다.
    - 삽입과 삭제를 할 때마다 동적으로 링크드 리스트의 크기가 결정되므로 전통적인 배열(Array)에 비해 처음부터 큰 공간을 할당할 필요가 없어진다.
    - 메모리 관리가 용이하다. (사실상 이게 가장 큰 이유이다.)

- 단점

- Doubly Linked List 코드

  ```python
  #Double Linked List
  
  class Node(object):
      def __init__(self, data, prev = None, next = None):
          self.data = data
          self.prev = prev
          self.next = next
  
  class DList(object):
      def __init__(self):
          self.head = Node(None)
          self.tail = Node(None, self.head)
          self.head.next = self.tail
          self.size = 0
      
      def listSize(self):
          return self.size
      
      def is_empty(self):
          if self.size != 0:
              return False
          else:
              return True
      
      def selectNode(self, idx):
          if idx > self.size:
              print("Overflow: Index Error")
              return None
          if idx == 0:
              return self.head
          if idx == self.size:
              return self.tail
          if idx >= self.size//2:
              target = self.head
              for _ in range(idx):
                  target = target.next
              return target
          else:
              target = self.tail
              for _ in range(self.size - idx):
                  target = target.prev
              return target
      
      def appendleft(self, value):
          if self.is_empty():
              self.head = Node(value)
              self.tail = Node(None, self.head)
              self.head.next = self.tail
          else:
              tmp = self.head
              self.head = Node(value, None, self.head)
              tmp.prev = self.head
          self.size += 1
              
      
      def append(self, value):
          if self.is_empty():
              self.head = Node(value)
              self.tail = Node(None, self.head)
              self.head.next = self.tail
          else:
              tmp = self.tail.prev
              newNode = Node(value, tmp, self.tail)
              tmp.next = newNode
              self.tail.prev = newNode
          self.size += 1
      
      def insert(self, value, idx):
          if self.is_empty():
              self.head = Node(value)
              self.tail = Node(None, self.head)
              self.head.next = self.tail
          else:
              tmp = self.selectNode(idx)
              if tmp == None:
                  return
              if tmp == self.head:
                  self.appendleft(value)
              elif tmp == self.tail:
                  self.append(value)
              else:
                  tmp_prev = tmp.prev
                  newNode = Node(value, tmp_prev, tmp)
                  tmp_prev.next = newNode
                  tmp.prev = newNode
          self.size += 1
          
      def delete(self, idx):
          if self.is_empty():
              print("Underflow Error")
              return
          else:
              tmp = self.selectNode(idx)
              if tmp == None:
                  return
              elif tmp == self.head:
                  tmp = self.head
                  self.head = self.head.next
              elif tmp == self.tail:
                  tmp = self.tail
                  self.tail = self.tail.prev
              else:
                  tmp.prev.next = tmp.next
                  tmp.next.prev = tmp.prev
              del(tmp)
              self.size -= 1
      
      def printlist(self):
          target = self.head
          while target != self.tail:
              if target.next != self.tail:
                  print(target.data, '<=> ', end='')
              else:
                  print(target.data)
              target = target.next
  ```