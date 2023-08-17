# 컬렉션 프레임워크 (Collection FrameWork)

---

### **Collection Framework**

- 다수의 데이터를 쉽고 효과적으로 처리할 수 있는 표준화된 방법을 제공하는 클래스의 집합을 의미
- 데이터를 저장하는 자료 구조와 데이터를 처리하는 알고리즘을 구조화하여 클래스로 구현해 놓은것
- 인터페이스(interface)를 사용하여 구현

### ****Collection Framework의 계층 구조****

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/def46fe7-4112-42c8-b8b8-06a99f62a0c6">

### **주요 인터페이스의 간략한 특징**

| 인터페이스 | 설명 | 구현 클래스 |
| --- | --- | --- |
| List<E> | 순서가 있는 데이터의 집합으로, 데이터의 중복을 허용함. | Vector, ArrayList, LinkedList, Stack, Queue |
| Set<E> | 순서가 없는 데이터의 집합으로, 데이터의 중복을 허용하지 않음. | HashSet, TreeSet |
| Map<K, V> | 키와 값의 한 쌍으로 이루어지는 데이터의 집합으로, 순서가 없음.
이때 키는 중복을 허용하지 않지만, 값은 중복될 수 있음. | HashMap, TreeMap, Hashtable, Properties |

### Collection 인터페이스

List와 Set 인터페이스의 많은 공통된 부분을 Collection 인터페이스에서 정의하고, 두 인터페이스는 그것을 상속받는다.

따라서 Collection 인터페이스는 컬렉션을 다루는데 가장 기본적인 동작들을 정의하고, 그것을 메소드로 제공하고 있다.

| 메소드 | 설명 |
| --- | --- |
| boolean add(E e) | 해당 컬렉션(collection)에 전달된 요소를 추가함. (선택적 기능) |
| void clear() | 해당 컬렉션의 모든 요소를 제거함. (선택적 기능) |
| boolean contains(Object o) | 해당 컬렉션이 전달된 객체를 포함하고 있는지를 확인함. |
| boolean equals(Object o) | 해당 컬렉션과 전달된 객체가 같은지를 확인함. |
| boolean isEmpty() | 해당 컬렉션이 비어있는지를 확인함. |
| Iterator<E> iterator() | 해당 컬렉션의 반복자(iterator)를 반환함. |
| boolean remove(Object o) | 해당 컬렉션에서 전달된 객체를 제거함. (선택적 기능) |
| int size() | 해당 컬렉션의 요소의 총 개수를 반환함. |
| Object[] toArray() | 해당 컬렉션의 모든 요소를 Object 타입의 배열로 반환함. |

---

## **List**

- 순서가 있는 데이터의 집합
- 데이터 중복을 허용한다.

### **구현 클래스**

- ArrayList
    - 내부적으로 배열을 이용하여 요소를 순차적으로 저장
    - 인덱스를 이용해 배열 요소에 빠르게 접근 가능
    - 요소의 추가 및 삭제 작업에 걸리는 시간이 김

---

- LinkedList
    - 배열을 이용하는 ArrayList 클래스의 단점을 극복하기 위해 고안
    - 내부적으로 연결 리스트를 이용하여 요소를 저장
    - 저장된 요소가 비순차적으로 분포
- 단일 연결 리스트(singly linked list)
    - 다음 요소를 가리키는 참조만을 가지는 연결 리스트
    - 요소의 저장, 삭제가 아주 빠르게 처리
    - 현재 요소에서 이전 요소로 접근하기 어려움
- 이중 연결 리스트(doubly linked list)
    - 이전 요소를 가리키는 참조를 가지는 이중 연결 리스트가 더 많이 사용

---

- Vector
    - ArrayList 클래스와 같은 동작을 수행하는 클래스
    - 현재에는 기존 코드와의 호환성을 위해서만 남아있음
    - Vector 클래스보다는 ArrayList 클래스를 사용하는 것이 좋음

---

- Stack
    - List 컬렉션 클래스의 Vector 클래스를 상속받음
    - 스택 메모리 구조의 클래스를 제공
    - 후입선출(LIFO)

### List 인터페이스 메소드

List 인터페이스는 Collection 인터페이스를 상속받으므로, Collection 인터페이스에서 정의한 메소드도 모두 사용할 수 있다.

| 메소드 | 설명 |
| --- | --- |
| boolean add(E e) | 해당 리스트(list)에 전달된 요소를 추가함. (선택적 기능) |
| void add(int index, E e) | 해당 리스트의 특정 위치에 전달된 요소를 추가함. (선택적 기능) |
| void clear() | 해당 리스트의 모든 요소를 제거함. (선택적 기능) |
| boolean contains(Object o) | 해당 리스트가 전달된 객체를 포함하고 있는지를 확인함. |
| boolean equals(Object o) | 해당 리스트와 전달된 객체가 같은지를 확인함. |
| E get(int index) | 해당 리스트의 특정 위치에 존재하는 요소를 반환함. |
| boolean isEmpty() | 해당 리스트가 비어있는지를 확인함. |
| Iterator<E> iterator() | 해당 리스트의 반복자(iterator)를 반환함. |
| boolean remove(Object o) | 해당 리스트에서 전달된 객체를 제거함. (선택적 기능) |
| boolean remove(int index) | 해당 리스트의 특정 위치에 존재하는 요소를 제거함. (선택적 기능) |
| E set(int index, E e) | 해당 리스트의 특정 위치에 존재하는 요소를 전달받은 객체로 대체함. (선택적 기능) |
| int size() | 해당 리스트의 요소의 총 개수를 반환함. |
| Object[] toArray() | 해당 리스트의 모든 요소를 Object 타입의 배열로 반환함. |

---

## Stack 과 Queue

### **Stack<E> 클래스**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/73ce7ded-ce69-4f50-ad0f-4839ac34e1ba">

Stack 클래스는 스택 메모리 구조를 표현하기 위해, Vector 클래스의 메소드를 5개만 상속받아 사용한.

| 메소드 | 설명 |
| --- | --- |
| boolean empty() | 해당 스택이 비어 있으면 true를, 비어 있지 않으면 false를 반환함. |
| E peek() | 해당 스택의 제일 상단에 있는(제일 마지막으로 저장된) 요소를 반환함. |
| E pop() | 해당 스택의 제일 상단에 있는(제일 마지막으로 저장된) 요소를 반환하고, 해당 요소를 스택에서 제거함. |
| E push(E item) | 해당 스택의 제일 상단에 전달된 요소를 삽입함. |
| int search(Object o) | 해당 스택에서 전달된 객체가 존재하는 위치의 인덱스를 반환함.
이때 인덱스는 제일 상단에 있는(제일 마지막으로 저장된) 요소의 위치부터 0이 아닌 1부터 시작함. |

### Queue<E> 인터페이스

클래스로 구현된 스택과는 달리 자바에서 큐 메모리 구조는 별도의 인터페이스 형태로 제공됩니다.

이러한 Queue 인터페이스를 상속받는 하위 인터페이스는 다음과 같다.

- Deque<E>
- BlockingDeque<E>
- BlockingQueue<E>
- TransferQueue<E>

따라서 Queue 인터페이스를 직간접적으로 구현한 클래스는 상당히 많다.

그중에서도 Deque 인터페이스를 구현한 LinkedList 클래스가 큐 메모리 구조를 구현하는 데 가장 많이 사용됩니다.

큐 메모리 구조는 선형 메모리 공간에 데이터를 저장하면서 선입선출(FIFO)의 시멘틱을 따르는 자료 구조다.

즉, 가장 먼저 저장된(push) 데이터가 가장 먼저 인출(pop)되는 구조다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/9edfe5b7-80c1-44ce-a1ab-a9f1cb3616c9">

Queue 인터페이스는 큐 메모리 구조를 표현하기 위해, 다음과 같은 Collection 인터페이스 메소드만을 상속받아 사용한다.

| 메소드 | 설명 |
| --- | --- |
| boolean add(E e) | 해당 큐의 맨 뒤에 전달된 요소를 삽입함.
만약 삽입에 성공하면 true를 반환하고, 큐에 여유 공간이 없어 삽입에 실패하면 IllegalStateException을 발생시킴. |
| E element() | 해당 큐의 맨 앞에 있는(제일 먼저 저장된) 요소를 반환함. |
| boolean offer(E e) | 해당 큐의 맨 뒤에 전달된 요소를 삽입함. |
| E peek() | 해당 큐의 맨 앞에 있는(제일 먼저 저장된) 요소를 반환함.
만약 큐가 비어있으면 null을 반환함. |
| E poll() | 해당 큐의 맨 앞에 있는(제일 먼저 저장된) 요소를 반환하고, 해당 요소를 큐에서 제거함.
만약 큐가 비어있으면 null을 반환함. |
| E remove() | 해당 큐의 맨 앞에 있는(제일 먼저 저장된) 요소를 제거함. |