# 스택 (Stack)

## 1. 정의

> LIFO 원칙을 따르는 선형 자료구조

- 후입선출 (LIFO, Last In First Out)

"가장 나중에 들어간 데이터가 가장 먼저 나온다"

- 추상 자료형(ADT, Abstract Data Type)

"데이터 구조의 논리적인 특성을 정의하지만 직접적인 구현은 추상화 하는 것"

<br>

## 2. 특징

- 스택은 배열처럼 데이터를 List 형태로 저장

- 데이터는 스택의 끝에서만 삽입 가능 => `push()`

- 데이터는 스택의 끝에서만 삭제 가능 => `pop()`

- 스택의 마지막 요소만 읽을 수 있음 => `peek()`

<br>

## 3. Implementation in JS

- Stack class 생성
```javascript
class Stack {
  constructor() {
    this._items = [];
  }

  push(item) {
    this._items.push(item);
  }

  pop() {
    this._items.pop();
  }

  peek() {
    // return this._items.at(1);
    return this._items[this._items.length-1];
  }
}
```

<br>

## 4. 시간 복잡도

`push()` : O(1)

`pop()` : O(1)

`peek()` : O(1)  
