# 큐 (Queue)

## 1. 정의

> FIFO 원칙을 따르는 선형 자료구조

- 선입선출 (FIFO, First In First Out)

"가장 먼저 들어간 데이터가 가장 먼저 나온다"


- ADT (추상 자료형)이다

<br>

## 2. 특징

- List 배열 형태로 사용
  
- 데이터는 큐의 맨 뒤에서 요소 추가 가능 => `enqueue()`

- 데이터는 큐의 맨 앞에서 요소 제거 가능 => `dequeue()`

<br>

## 3. Implementation in JS

```javascript
class Queue {
  constructor() {
    this._items = [];
  }

  enqueue(item) {
    this._items.push(item);
  }

  dequeue() {
    if (this.isEmpty()) {
      console.log("Queue is empty");
      return;
    }

    return this._items.shift();
  }

  isEmpty() {
    return this.size() === 0;
  }

  size() {
    return this._items.length;
  }
}
```

<br>

## 4. 시간 복잡도

`enqueue()` : O(1)

`dequeue()` : O(N) (배열의 모든 요소를 한 칸씩 이동시켜야함)

만약 배열이 아닌 **연결리스트** 사용 시 => `dequeue()`도 O(1) 소요!
