# 6장 - 데이터 타입

### 들어가기에 앞서

- 자바스크립트의 7가지 데이터 타입 중 객체를 제외한 나머지 6가지는 원시 타입이다.
    - 원시 타입: 숫자 타입, 문자열 타입, 불리언 타입, null 타입, undefined 타입, 심벌 타입(es6)
    - NaN도 숫자 타입이다. `typeof NaN // --> 'number'`
- **각각의 데이터 타입 모두 값을 생성한 목적과 용도가 다르다.**

```jsx
1 === '1'; // false
```

- 숫자 타입 값의 주된 용도: 산술 연산
- 문자열 타입 값의 주된 용도: 텍스트를 화면에 출력
- 각 타입마다 차지하는 메모리 공간, 메모리에 저장되는 2진수, 해석 방식 3가지 모두 다르다.

## 6.1 숫자 타입

### 6.1.1 정수, 실수 리터럴

```jsx
// 셋 모두 동일하게 숫자 타입으로 해석된다.
var integer = 10;   // 정수
var double = 10.12; // 실수
var negative = -20; // 음의 정수
```

- 타 언어와의 차이: 정수, 실수, 소수 등 **수의 종류를 구분하지 않고** **모두 숫자 타입** 하나로 본다. (배정밀도 64비트 부동소수점 형식)

### 6.1.2 진수 리터럴

```jsx
// 2, 8, 16진수 리터럴이 있지만 참조시 해석은 모두 10진수로 해석된다.
var binary = 0b01000001; // 2진수 리터럴
var octal = 0o101;       // 8진수 리터럴
var hex = 0x41;          // 16진수 리터럴

console.log(binary); // 65
console.log(octal);  // 65
console.log(hex);    // 65
console.log(binary === octal); // true
console.log(octal === hex); // true
```

### 6.1.3 특이한 값

- 양의 무한대: `Infinity`
- 음의 무한대: `-Infinity`
- 연산 불가(수가 아님): `NaN`

```jsx
// 0으로 나누기는 +0이든 -0이든 수학적으로 성립되지 않는 개념이다.
console.log(10 / 0);    // Infinity
console.log(10 / -0);   // -Infinity
console.log(1 - 'abc'); // NaN
```

## 6.2 문자열 타입 + 6.3 템플릿 리터럴

- 큰 따옴표, 작은 따옴표, 백틱으로 문자를 감싸 표현한다.
- ES6에서 백틱으로 감싸는 템플릿 리터럴이 도입됨.
    - 개행문자 없이 줄 바꿈 가능
    - ${}로 중괄호 안에 변수나 표현식을 넣어 값을 문자로 출력 가능.
    
    ```jsx
    // 이스케이프 시퀀스 없이도 줄바꿈과 공백 적용.
    let str = `<body>
    	<div></div>	
    </body>`;
    
    console.log(str);
    /**
    <body>
    	<div></div>	
    </body>
    */
    ```
    

## 6.4 불리언 타입

- `true` 또는 `false` 두가지 값만 존재한다.
- 조건문에서 자주 사용.

## 6.5 undefined 타입

- 값의 종류는 `undefined` 하나 뿐이다.
- 변수를 선언한 이후 값을 할당하지 않은 경우 참조시 `undefined` 가 반환된다.
    - 변수 선언문은 표현식이 아닌 문이다.

## 6.6 null 타입

- 값의 종류는 `null`  하나뿐이다.
- `NaN` 처럼 대소문자를 구분하기 때문에 Null이나 NULL이 아닌 `null` 로 써야 한다.
- 변수에 값이 **명시적으로** 없음을 알리고자 할 때 주로 사용한다.
    - 이전에 참조하던 값을 더이상 참조하지 않겠다는 의미.
- 쿼리셀렉터가 해당 html 요소를 찾지 못할 경우에도 에러가 나오는 대신 `null` 을 반환한다.

## 6.7 심벌 타입

- es6에서 추가된 변경이 불가능한 원시 타입 값이다.
- 일반적으로 다른 원시 값들은 리터럴을 통해 생성하지만 심벌은 Symbol 함수를 호출해 생성한다.
- 다른 값과 중복이 되지 않는 유일무이한 값.

## 6.8 객체 타입

[별도 문서로 정리](https://ryan-kim-dev.tistory.com/63)

## 6.9 데이터 타입의 필요성

### 6.9.1 데이터 타입에 의한 메모리 공간의 확보와 참조

값을 할당 시 - 값을 저장할 때 확보해야 하는 메모리 공간의 크기를 결정하기 위해

- 변수에 할당되는 값의 종류에 따라 확보해야 할 메모리 공간의 크기도 달라진다.
    - ex: 숫자는 8바이트, 문자는 2바이트

값을 참조 시 - 한번에 읽어 들여야 할 메모리 공간의 크기를 결정하기 위해

- 읽어들여야 할 메모리 공간의 크기를 알아야 한다.

메모리에서 읽어들인 2진수를 어떻게 해석할지 결정하기 위해

 

## 6.10 동적 타이핑

- 자바스크립트의 변수는 데이터 타입을 갖지 않는, 즉 변수에 어떤 데이터 타입의 값이라도 자유롭게 할당할 수 있는 동적 타입 언어이다.
- 반면 c나 자바 같은 정적 타입 언어는 변수 선언시 데이터 타입을 사전에 선언해야 한다.(명시적 타입 선언)