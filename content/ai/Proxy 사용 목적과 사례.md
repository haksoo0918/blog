---
tags:
  - javascript
  - proxy
---

## 1. Proxy 한 줄 요약

> **"객체 본체는 순수 데이터만 들고 있게 두고, 중간 대리인(Proxy)이 읽기·쓰기·삭제 등 모든 접근을 가로채서(Intercept) 부가 작업을 처리하는 도구"**

## 2. 왜 객체에 직접 안 만들고 Proxy를 쓸까? (직접 구현 vs Proxy)

Proxy를 쓰는 가장 핵심적인 이유는 **'데이터'와 '제어 로직'의 완벽한 분리**입니다.

### ① 객체 직접 구현 방식 (결합도가 높은 방식)

객체 내부에서 검증이나 UI 업데이트 같은 부가 기능을 스스로 처리하도록 만든 형태입니다.

```javascript
const user = {
  _age: 0,
  get age() { 
    return this._age; 
  },
  set age(val) {
    if (val < 0) throw new Error("음수 불가"); // 객체 내부에 검증 로직 침범
    this._age = val;
    updateUI(); // 객체 내부에 UI 업데이트 로직까지 강하게 결합됨
  }
};
```

- **문제점**: 데이터 구조만 가져야 할 객체가 검증, UI 업데이트 등 온갖 부가 기능까지 짊어지게 되어 코드가 비대해지고 복잡해집니다.

### ② Proxy 활용 방식 (관심사 분리 방식)

원본 객체는 순수한 데이터만 유지하고, 부가 작업은 외부 대리인(Proxy)이 담당합니다.

```javascript
// 1. 원본 객체는 순수 데이터 구조만 유지
const user = { age: 0 };

// 2. 부가 기능(검증, UI 업데이트 등)은 Proxy 핸들러가 전담
const userProxy = new Proxy(user, {
  set(target, key, value) {
    if (key === 'age' && value < 0) {
      throw new Error("음수 불가");
    }
    target[key] = value;
    updateUI(); // 원본 객체를 건드리지 않고 외부에서 기능 주입
    return true;
  }
});
```

- **장점**:
    
    - 원본 데이터(`user`)의 코드가 매우 깨끗해집니다.
    - 기존 방식(`Object.defineProperty`)과 달리 **나중에 동적으로 추가되는 속성이나 삭제 작업(`delete`)까지 일괄 포획**합니다. (Vue 3의 핵심 원리)
    - 하나 만들어둔 핸들러 로직을 여러 객체에 그대로 재사용할 수 있습니다.

## 3. 대표적인 실무 활용 사례 4가지

### ① 반응형(Reactivity) 상태 관리 (Vue 3 핵심 원리)

```javascript
function createReactiveObject(target, callback) {
  return new Proxy(target, {
    set(target, key, value) {
      const oldValue = target[key];
      target[key] = value;
      if (oldValue !== value) callback(key, value); // 변경 시 UI 업데이트
      return true;
    }
  });
}

const state = createReactiveObject({ count: 0 }, (key, val) => {
  console.log(`UI 업데이트: ${key} -> ${val}`);
});

state.count = 1; // "UI 업데이트: count -> 1"
```

### ② 데이터 검증 (Data Validation)

```javascript
const userSchema = {
  set(target, key, value) {
    if (key === 'age' && (typeof value !== 'number' || value < 0)) {
      throw new TypeError('나이는 0 이상의 숫자여야 합니다.');
    }
    target[key] = value;
    return true;
  }
};

const user = new Proxy({}, userSchema);
user.age = 25; // 정상
// user.age = -5; // Error 발생
```

### ③ 언어 동작 재정의 (음수 인덱스 배열)

```javascript
const createNegativeArray = (arr) => {
  return new Proxy(arr, {
    get(target, prop) {
      const index = Number(prop);
      if (index < 0) prop = String(target.length + index); // 음수면 뒤에서부터 계산
      return Reflect.get(target, prop);
    }
  });
};

const array = createNegativeArray(['A', 'B', 'C']);
console.log(array[-1]); // 'C'
```

### ④ 접근 제어 및 로깅 (Logging)

```javascript
const withLogging = (target) => {
  return new Proxy(target, {
    get(target, key) {
      console.log(`[READ] ${String(key)}`);
      return target[key];
    },
    set(target, key, value) {
      console.log(`[WRITE] ${String(key)} = ${value}`);
      target[key] = value;
      return true;
    }
  });
};
```

## 4. 최종 핵심 요약

|**구분**|**내용**|
|---|---|
|**핵심 개념**|객체 앞단을 가로채서 읽기/쓰기 동작을 처리하는 대리인|
|**사용 이유**|객체 내부 코드를 더럽히지 않고, 검증/감지/제어 로직을 독립적으로 분리·주입하기 위해|
|**주의 사항**|트랩 실행 시 오버헤드가 발생하므로, 엄청나게 빠른 반복문 안에서의 남용은 지양할 것|

---

> 추가. Proxy에서 "트랩(Trap) 실행 시 오버헤드가 발생한다"는 말은...?

쉽게 말해 "객체에 접근할 때 중간에서 일을 처리하는 과정(함수 호출)이 추가되기 때문에 메모리와 시간이 더 든다 - 오버헤드(자원 손실)"는 뜻입니다.

## 1. 일반 접근 vs Proxy 접근 방식 차이

### ① 일반 객체 접근 (Engine Direct)

```javascript
const user = { age: 25 };
const myAge = user.age;
```

- **동작**: JavaScript 엔진(V8 등)이 메모리 주소를 찾아 **즉시(Direct) 데이터 값을 읽어옵니다.**
- **비용**: 거의 0에 가까운 최적화된 연산입니다.
### ② Proxy 객체 접근 (Trap Execution)

```javascript
const userProxy = new Proxy({ age: 25 }, {
  get(target, key) {
    return target[key]; // <--- 이 'get' 함수가 바로 '트랩(Trap)'입니다.
  }
});
const myAge = userProxy.age;
```

- **동작**:
    
    1. `userProxy.age`를 읽으려고 시도합니다.
    2. 엔진이 Proxy 객체임을 감지하고 접근을 가로챕니다.
    3. `get`이라는 **트랩(함수)을 생성 및 실행**합니다.
    4. 트랩 내부 코드(`return target[key]`)가 실행됩니다.
    5. 최종 결과를 반환합니다.
        
- **비용**: 단순 메모리 참조가 아니라 '함수 호출 및 Context 생성'이라는 단계가 추가됩니다.

## 2. '트랩'이라는 단어의 뜻

Proxy에서 `get`, `set`, `has`, `deleteProperty` 등을 트랩(Trap)이라고 부릅니다.

운영체제나 프로그래밍에서 트랩은 "어떤 이벤트가 발생했을 때 이를 가로채서 특정 코드로 제어권을 넘기는 장치"를 말합니다.

즉, `user.age = 30`이라고 썼을 때 JavaScript 엔진이 그냥 넘어가지 않고 미리 설정해 둔 트랩 함수로 퐁당 빠져서 그 안의 코드를 실행하기 때문에 붙은 이름입니다.

## 3. 언제 문제가 될까? (실제 성능 차이)

일반적인 웹 애플리케이션 개발(버튼 클릭, 폼 입력, API 데이터 처리 등)에서는 이 차이를 **사람이 전혀 체감할 수 없습니다.**

하지만 **극단적으로 반복되는 연산**에서는 확연한 성능 차이가 납니다.

```javascript
// 1,000,000번 반복하는 루프 테스트

// [Case 1] 일반 객체
for (let i = 0; i < 1000000; i++) {
  const a = obj.count; // 엔진이 최고 수준으로 최적화(JIT 컴파일)함
}

// [Case 2] Proxy 객체
for (let i = 0; i < 1000000; i++) {
  const a = proxyObj.count; // 루프를 돌 때마다 get() 트랩 함수를 1,000,000번 호출함
}
```

- **일반 객체**: 엔진 최적화(JIT Compilation) 덕분에 거의 몇 밀리초(ms) 만에 끝납니다.
- **Proxy 객체**: 루프마다 함수 호출 컨텍스트가 만들어지고 트랩 로직을 거쳐야 하므로 수배에서 수십 배까지 시간이 더 걸릴 수 있습니다.

## 4. 결론

- **오버헤드란?**: 단순 데이터 조회/수정 사이에 **'가로채는 함수(트랩) 호출 과정'이 추가되어 발생하는 실행 시간 및 메모리 비용**.
- **실무적 관점**: 일반적인 웹/앱 개발(유효성 검사, 상태 관리 등)에서는 Proxy의 오버헤드가 무시할 수 있는 수준이므로 안심하고 사용하셔도 됩니다. 단, **대용량 배열을 반복 순회하는 3D 그래픽 연산이나 복잡한 수학 계산 루프 내부** 같은 특수한 상황에서만 주의하면 됩니다.