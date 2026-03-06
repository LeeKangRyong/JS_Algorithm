# 연결 리스트 (Linked List)

## 1. 정의

> 각 요소를 포인터로 연결하여 관리하는 선형 자료구조

<img width="50%" alt="linked_list_img" src="https://github.com/user-attachments/assets/01ce3637-4a34-454e-9b71-32a670d15b24" />

- 노드 (Node) : 각 요소  
`| 데이터 영역 | 포인터 |` (포인터는 다음 노드를 가리킴)

- 헤드 (Head) : 첫 번째 노드

- 테일 (Tail) : 포인터 영역이 `NULL`로 가리키는 곳 or 갈 곳이 없는 마지막

<br>

## 2. 특징

- 배열과 다르게 **요소를 제한 없이 추가 가능**

- 연속 배치가 아닌 퍼져있는 데이터에서 **포인터**를 통해 다음 노드를 알 수 있음

<br>

- **요소 찾기 (Search) 과정** (단일 연결 리스트 기준)

```bash
1. Head에서 시작
2. next 포인터를 따라가며 원하는 값을 가진 노드 만날 때까지 순차 탐색
```

- **요소 삽입 (Insert) 과정** (단일 연결 리스트 기준)

```bash
1. 새 node 생성
2. 새 node의 next가 이전 node의 next를 가리키게 함
3. 이전 노드의 next가 새 node를 가리키게 함
```

- **요소 삭제 (Delete) 과정** (단일 연결 리스트 기준)

```bash
1. Head에서 시작
2. 삭제할 노드의 바로 '이전 노드(previousNode)'를 찾을 때까지 탐색
3. 이전 노드의 next를 삭제할 노드의 next로 변경 (중간 노드 건너뛰기)
4. 만약 삭제한 노드가 Tail이었다면, 이전 노드를 새로운 Tail로 지정
```

<br>

## 3. 종류

<img width="80%" alt="lined_list_types" src="https://github.com/user-attachments/assets/79bf4747-2f4c-42fb-8b30-190b8db9c295" />


- 단일 연결 리스트 (Singly Linked List)

> Head부터 Tail까지 단방향으로 이어짐 

- 이중 연결 리스트 (Doubly Linked List)

> 양 방향으로 이어지는 연결 리스트
> 
> 단일 연결 리스트에서 이전 노드를 가리키는 포인터가 추가됨

- 원형 연결 리스트 (Circular Linked List)

> 단일 or 이중 연결 리스트에서 Tail이 Head로 연결되는 리스

<br>

## 4. Implementation in JS

```javascript
// 노드 클래스
class Node {
  constructor(value) {
    this.value = value; // 데이터 영역
    this.next = null; // 다음 노드 가리키는 포인터
  }
}

// 단일 연결 리스트
class SinglyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  // 요소 찾기
  search(value) {
    let currentNode = this.head; // 헤드에서 찾기 시작
    while (currentNode.value !== value) { // 현재 노드의 값이 찾는 값이 아니면
      currentNode = currentNode.next; // 다음 노드로 넘어감
    }

    return currentNode; // 찾았으면 해당 노드 반환
  }

  // 요소 추가
  append(newValue) {
    const newNode = new Node(newValue); // newValue 값 가진 노드 생성

    // 리스트가 비어있을 때, head 및 tail을 newNode로 설정 
    if (this.head === null) {
      this.head = newNode;
      this.tail = newNode;

    // 리스트가 비어있지 않을 때, tail에 newNode를 놓으면 됨
    } else {
      this.tail.next = newNode; 
      this.tail = newNode;
    }
  }

  // 요소 삽입 (특정 노드 뒤에 newValue 값 가진 노드 생성 후 삽입)
  insert(node, newValue) {
    const newNode = new Node(newValue);

    newNode.next = node.next; // 1. newNode가 node의 next를 가리키게 하기
    node.next = newNode; // 2. node가 newNode를 가리키게 함으로써 뒤로 가게 하기
  }

  // 요소 삭제
  delete(value) {
    if (!this.head) return; // 리스트가 비어있으면 종료

    // 1. 삭제할 값이 헤드인 경우
    if (this.head.value === value) {
      this.head = this.head.next;

      // 만약 노드가 하나뿐이었다면 tail도 null로 변경
      if (this.head === null) this.tail = null;
      return;
    }

    // 2. 그 외의 경우 (이전 노드 찾기)
    let previousNode = this.head;

    while (previousNode.next !== null && previousNode.next.value !== value) {
      previousNode = previousNode.next;
    }

    // 3. 찾았을 경우 연결 수정
    if (previousNode.next !== null) {
      // 삭제될 노드가 마지막(tail)이었다면 tail을 이전 노드로 옮김
      if (previousNode.next === this.tail) {
        this.tail = previousNode;
      }

      // 건너뛰기 수행
      previousNode.next = previousNode.next.next;
    }
  }
}
```

<br>

## 4. 시간 복잡도

탐색 (Search) : O(n)

삽입 (Insert) : O(1)

삭제 (Delete) - O(n) => O(n) (head 찾기) * O(1) (pointer 변경)

(위치를 아는 경우 삭제도 O(1))

