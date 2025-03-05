1. 위 코드에서 콘솔창에 찍히는 내용을 각각 적어주세요.

```javascript
function memoizedAdd() {
  let cache = {};
  return function (num) {
    if (num in cache) {
      console.log("캐시에서 가져옴!");
      return cache[num];
    }
    console.log("새로 계산!");
    cache[num] = num + 10;
    return cache[num];
  };
}

const add10 = memoizedAdd();
console.log(add10(5));
console.log(add10(5));
console.log(add10(10));
console.log(add10(10));
```

- 정답
  1. "ReferenceError"
  2. "새로 계산!"
  3. 15
  4. "캐시에서 가져옴"
  5. 15
  6. "새로 계산!"
  7. 20
  8. "캐시에서 가져옴"
  9. 20
