### 데이터 타입

구분 | 데이터 타입 | 설명
--|--|--
| 원시타입 | 숫자(number) 타입 | 숫자, 정수와 실수 구분 없이 하나의 숫자 타입만 존재
| |문자열(string) 타입 | 문자열
| |불리언(boolean) 타입 | 논리적 참(true)과 거짓(false)
| |undefined 타입 | var 키워드로 선언된 변수에 암묵적으로 할당되는 값
| |null 타입 | 값이 없다는 것을 의도적으로 명시할 때 사용하는 값
| | 심벌(symbol) 타입 | ES6에서 추가된 7번째 타입
| | Bigint 타입 | ES11에서 추가된 8번째 타입
|객체타입 | | 객체, 함수, 배열 등
자바스크립트의 모든 값은 데이터 타입을 갖습니다. 자바스크립트(ES11)는 8개의 데이터 타입을 제공하며, 7개의 타입은 원시(primitive) 타입과 객체(object/reference) 타입으로 분류할 수 있습니다.

### 1. 숫자 타입
자바스크립트는 모든 수를 실수로 처리하며, 정수만 표현하기 위한 데이터 타입은 별도로 존재하지 않습니다. 이는 정수로 표시된다 해도 사실은 실수라는 것을 의미합니다. 
```javascript
// 숫자 타입은 모두 실수로 처리됩니다.
console.log(1 === 1.0); //true
```
정수, 실수, 2진수, 8진수, 16진수, 리터럴은 모두 메모리에 **배정밀도 64비트 부동소수점 형식의 2진수**로 저장됩니다. 자바스크립트는 2진수, 8진수, 16진수에 대한 데이터 타입을 제공하지 않기 때문에 이들 값을 참조하면 모두 10진수로 해석됩니다. 
- 배정밀도 64비트 부동소수점이란
  - <a href="https://ko.wikipedia.org/wiki/%EB%B6%80%EB%8F%99%EC%86%8C%EC%88%98%EC%A0%90" target = "_blank">부동소수점</a> 방식은 실수를 컴퓨터상에서 근사하여 표현할 때 <u>소수점의 위치를 고정하지 않고 그 위치를 나타내는 수를 따로 적는 것</u>을 말합니다. 
  컴퓨터가 이러한 방식을 택하는 이유는 효율적인 메모리 사용 때문입니다.
<a href="https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%9A%A8%EC%88%AB%EC%9E%90" target="_blank">유효숫자</a>를 나타내는 `가수`와 소수점의 위치를 풀이하는 `지수`나누어 표현합니다.

 숫자 12345678.9와 1.23456789의 예시를 들어보겠습니다.

 방식 | 12345678.9와 1.23456789의 경우 | 데이터 저장 방식
--:|--:|--:
고정 소수점 방식 | 12345678.9 | 정수 부분 8자리 + 소수 1자리
부동 소수점 방식 | 1.23456789 x 10^8 | 가수 부분 9자리 + 지수 1자리
--|--|--
고정 소수점 방식 | 1.23456789 | 정수 부분 1자리 + 소수 8자리
부동 소수점 방식 | 1.23456789 x 10^0 | 가수 부분 9자리 + 지수 1자리
고정 소수점 방식으로는 1.23456789 ~ 12345678.9까지의 모든 숫자를 처리하기 위해 정수 부분 8자리 + 소수 8자리가 필요합니다. 그러나 부동 소수점 방식에서는 가수 부분(1.23456789를 저장하는 곳)이 9자리, 지수(10의 제곱을 저장하는 자리)1자리로 총 10자리가 필요합니다.


- 숫자 타입은 추가적으로 아래 세 가지의 특별한 값도 표현할 수 있습니다.
`Infinity`, `-Infinity`, `NaN`
```javascript
console.log(10/0); // Infinity: 양의 무한대
console.log(10/-0); // -Infinity: 음의 무한대
console.log(1*'String'); // NaN: 산술 연산 불가(not-a-number)
```
### 2. 문자열 타입
문자열은 0개 이상의  <a href="https://ko.wikipedia.org/wiki/UTF-16" target="_blank">16비트 유니코드</a> 문자의 집합으로 전 세계 대부분의 문자를 표현할 수 있습니다.
문자열은 작은따옴표(''), 큰따옴표("") 또는 백틱(`)으로 텍스트를 감싸서 사용합니다.

```javascript
var string;
string = '문자열'; // 작은따옴표
string = "문자열"; // 큰따옴표
string = `문자열`; // 백틱(ES6)

string = '작은따옴표로 감싼 문자열 내의 "큰따옴표"는 문자열로 인식된다.';
string = "큰따옴표로 감싼 문자열 내의 '작은따옴표'는 문자열로 인식된다.";
```
다른 타입의 값과 달리 문자열을 따옴표로 감싸는 이유는 키워드나 식별자 같은 토큰과 구분하기 위해서 입니다.
```javascript
// 따옴표로 감싸지 않은 hello를 식별자로 인식합니다.
var string = hello; // ReferenceError: hello is not defineds
```
그리고 만약 따옴표로 문자열을 감싸지 않는다면 스페이스와 같은 공백 문자도 포함시킬 수 없습니다.

### 3. 템플릿 리터럴
템플릿 리터럴(template literal)은 ES6부터 도입된 새로운 문자열 표기법입니다. 템플릿 리터럴은 <u>멀티라인 문자열(multi-line string), 표현식 삽입(expression interpolation), 태그드 탬플릿(tagged template)</u> 등 편리한 문자열 처리 기능을 제공합니다.
템플릿 리터럴은 **백틱(`)**을 사용해 표현하며, 런타임에 일반 문자열로 변환되어 처리됩니다.

1. 멀티라인 문자열
일반 문자열 내에서는 줄바꿈(개행)이 허용되지 않습니다.

```javascript
var str = "hello
world" ;
// SyntaxError: Invalid or unexpected token
```
따라서 일반 문자열 내에서 줄바꿈 등의 공백(white space)을 표현하려면 백슬래시(\)로 시작하는 이스케이프 시퀀스(escape sequence)를 사용해야 합니다.

이스케이프 시퀀스 | 의미
--|--|
\0 | Null
\b | 백스페이스
\f | 폼 피드(Form Feed): 프린터로 출력할 경우 다음 페이지의 시작 지점으로 이동
\n | 개행(LF, Line Feed): 다음 행으로 이동
\r | 개행(CR, Carriage Return): 커서를 처음으로 이동
\t | 탭(수평)
\v | 탭(수직)
\uXXXX | 유니코드. 예를 들어 '\u0041'은 'A'
\' | 작은따옴표
\" | 큰따옴표
\\ | 백슬래시


```javascript
// 일반 문자열 표기시 ("", '', ``)
var template = '<ul>\n\t<li><a href="#">Home</a></li>\n</ul>'
console.log(template);
// 출력 결과
<ul>
  <li><a href="#">Home</a></li>
</ul>

// 템플릿 리터럴 표기 시 (백틱(`))
var template = `<ul>
<li><a href="#">Home</a></li>
</ul>`	
console.log(template);
// 출력 결과
<ul>
  <li><a href="#">Home</a></li>
</ul>
```
2. 표현식 삽입
일반 문자열은 문자열 연산자 +를 사용해 연결할 수 있습니다. 
템플릿 리터럴 내에서는 ** 표현식 삽입(expression interpolation) **을 통해 간단히 문자열을 삽입할 수 있습니다.
** 표현식을 삽입하려면 ${}으로 표현식을 감싸야합니다. ** 이때 표현식의 평가 결과가 문자열이 아니더라도 강제로 문자열 타입으로 변환되어 삽입됩니다.
```javascript
var first = 'Ung-mo';
var last = 'Lee';

// ES5: 문자열 연결
console.log('My name is ' + first + ' ' + last + '.');
// My name is Ung-mo Lee.

// 템플릿 리터럴 표기 시 (백틱(`))
var first = 'Ung-mo';
var last = 'Lee';

// ES5: 문자열 연결
console.log(`My name is ${first} ${last}.`);
// My name is Ung-mo Lee.
```

### 4. 불리언 타입
불리언 타입의 값은 놀리적 참, 거짓을 나타내는 true와 false뿐입니다.
```javascript
var foo = true;
console.log(foo); // true

foo = false;
console.log(foo); // false
```

### 5. undefined 타입
undefined 타입의 값은 undefined가 유일합니다.

undefined는 개발자가 의도적으로 할당하는 값이 아니라 자바스크립트 엔진이 변수를 초기화할 때 사용하는 값입니다. 
다시 말해, 변수 선언에 의해 확보된 메모리 공간을 처음 할당이 이뤄질 때까지 빈 상태(대부분 비어 있지 않고 쓰레기 값(garbage value)이 들어 있다)로 내버려두지 않고 자바스크립트 엔진이 undefined로 초기화합니다.
따라서, 변수를 선언한 이후 값을 할당하지 않은 변수를 참조하면 undefined가 반환됩니다.

```javascript
var foo;
console.log(foo); // undefined
```
undefined는 자바스크립트 엔진이 변수를 초기화하는 데 사용하기 때문에 개발자가 의도적으로 변수에 할당하는 건 본래의 취지와 어긋나므로 권장되지 않습니다.
** 따라서, 변수에 값이 없다는 것을 명시하고자 할때는 null을 할당합니다. **

### 6. null 타입
null 타입의 값은 null이 유일합니다.
변수에 null을 할당하는 것은 변수가 이전에 참조하던 값을 더 이상 참조하지 않겠다는 의미입니다.
프로그래밍 언어에서 null은 변수에 값이 없다는 것을 의도적으로 명시할 때 사용합니다. 함수가 유효한 값을 반환할 수 없는 경우 명시적으로 	null을 반환하기도 합니다.

현재까지 논의되고 있는 null과 undefined의 사용에 대해서 다음을 참조하기실 바랍니다.
<a href="" target="_blank">null vs undefined</a> 

### 7. 심벌 타입
심벌(symbol)은 ES6에서 추가된 7번째 타입으로, 변경 불가능한 원시 타입의 값입니다. 따라서 주로 이름이 충돌할 위험이 없는 객체의 유일한 프로퍼티 키를 만들기 위해 사용합니다. 심벌 이외의 원시 값은 리터럴을 통해 생성하지만 심벌은 Symbol 함수를 통해 호출해 생성합니다.

```javascript
// 심벌 값 생성
var key = Symbol('key');
console.log(typeof key); //symbol

// 객체 생성
var obj = {};

// 이름이 충돌할 위험이 없는 유일무이한 값인 심벌을 프로퍼티 키로 사용한다.
obj[key] = 'value';
console.log(obj[key]); // value
```

### 8. BitInt 타입
BitInt는 ES11에서 추가된 8번째 타입입니다. 숫자값을 안정적으로 나타낼 수 있는 최대치인 2^53-1보다 큰 정수를 표현할 수 있는 새로운 원시값입니다.
BigInt 값은 정수 리터럴의 뒤에 n을 붙이거나(10n) BigInt 함수를 호출(BigInt(10))해 생성할 수 있습니다.

---
자바스크립트의 데이터 타입은 크게 원시 타입과 객체 타입으로 분류됩니다.
** 중요한 것을 자바스크립트는 객체 기반의 언어이며, 자바스크립트를 이루고 있는 거의 모든 것이 객체라는 것입니다. **
위 7가지 데이터 타입 이외의 값은 모두 객체 타입입니다. 
객체 타입에 대한 설명은 추후 포스팅 예정입니다.

### 9. 데이터 타입의 필요성
- 값을 저장할 때 확보해야 하는 ** 메모리 공간의 크기 **를 결정하기 위해
- 값을 참조할 때 한 번에 읽어 들여야 할 **메모리 공간의 크기를 결정하기 위해**
- 메모리에서 읽어 들인 2진수를 어떻게 해석할지 결정하기 위해

1. 데이터 타입에 의한 메모리 공간의 확보와 참조
몇 바이트의 메모리 공간을 사용해야 낭비와 손실없이 데이터를 저장할 수 있을까요?

자바스크립트 엔진은 데이터 타입, 즉 값의 종류에 따라 정해진 크기의 메모리 공간을 확보합니다. 즉, <u>변수에 할당되는 값의 데이터 타입에 따라 확보해야 할 메모리 공간의 크기가 결정됩니다.</u>
```javascript
var score = 100;
```
위 코드가 실행되면 자바스크립트 엔진은 리터럴 100을 숫자 타입의 값으로 해석하고 숫자 타입의 값 100을 저장하기 위해 8바이트(64비트)의 메모리 공간을 확보합니다. 그리고 100을 2진수로 저장합니다.

> 참고로 ECMAScript 사양은 문자열과 숫자 타입 외의 데이터 타입의 크기를 명시적으로 규정하고 있지는 않습니다. 따라서 문자열과 숫자 타입을 제외하고 데이터 타입에 따라 확보되는 메모리 공간의 크기는 자바스크립트 엔진 제조사의 구현에 따라 다를 수 있습니다.

자바스크립트 엔진이 값을 참조하려는 경우 위 식별자 score를 통해 숫자 값 100이 저장되어 있는 메모리 공간의 주소를 찾아갑니다. 
정확히 표현하자면 숫자 값 100이 저장되어 있는 메모리 공간의 선두 메모리 셀의 주소를 찾아갑니다.

이때, <u>값을 참조하려면 한 번에 읽어 들여야 할 메모리 공간의 크기, 즉 메모리 셀의 개수(바이트 수)를 알아야합니다.</u> 자바스크립트 엔진은 score 변수를 숫자 타입으로 인식하고 숫자 타입은 8바이트(64비트) 단위로 저장되므로 score 변수를 참조하면 8바이트(64비트) 단위로 메모리 공간에 저장된 값을 읽어들입니다.

<a href="https://ko.wikipedia.org/wiki/%EC%8B%AC%EB%B3%BC_%ED%85%8C%EC%9D%B4%EB%B8%94" target = "_blank">심벌 테이블 </a> 
>컴파일러 또는 인터프리터는 심벌 테이블이라고 부르는 자료 구조를 통해 식별자를 키로 바인딩된 값의 메모리 주소, 데이터 타입, 스코프 등을 관리합니다.

2. 데이터 타입에 의한 값의 해석
모든 값은 데이터 타입을 가지며, 메모리에 2진수, 즉 비트의 나열로 저장됩니다. <u>메모리에 저장된 값은 데이터 타입에 따라 다르게 해석될 수 있습니다.</u> 예를 들어, 메모리에 저장된 값 0100 0001을 숫자로 해석하면 65지만 문자열로 해석하면 'A'입니다.

### 10. 동적 타이핑
1. 동적 타입 언어와 정적 타입 언어
자바스크립트에서 변수는 데이터 타입을 가질까요?
기본적으로 변수는 타입을 갖지 않습니다. 현재 변수에 할당되어 있는 값에 의해 변수의 타입이 동적으로 결정됩니다.

- 정적 타입 언어(static/strong type)
C나 자바 같은 정적 타입 언어는 변수를 선언할 때 변수에 할당할 수 있는 값의 종류, 즉 데이터 타입을 사전에 선언해야 합니다. 이를 명시적 타입 선언(explicit type declaration)이라 합니다.
대표적인 언어로는 C, C++, JAVA, Kotlin, Go, Haskell 등이 있습니다.
```javascript
// c 변수에는 1바이트 정수 타입의 값(-128 ~ 127)만 할당할 수 있다.
char C;

// num 변수에는 4바이트 정수 타입의 값(-2,124,483,648 ~ 2,124,483,647) 만 할당할 수 있다.
int num;
```
정적 타입 언어는 변수의 타입을 변경할 수 없으며, 변수에 선언한 타입에 맞는 값만 할당할 수 있습니다. 정적 타입 언어는 컴파일 시점에 **타입 체크**(선언한 데이터 타입에 맞는 값을 할당했는지 검사하는 처리)를 수행합니다. 
타입 체크에 통과하지 못하면 에러를 발생시키고 프로그램의 실행 자체를 막습니다.
이를 통해 안정적인 코드의 구현을 통해 런타임에 발생하는 에러를 줄입니다.

- 동적 타입 언어(dynamic/weak type)
자바스크립트의 변수는 선언이 아닌 할당에 의해 타입이 결정(타입 추론(type inference))됩니다. 그리고 재할당에 의해 변수의 타입은 언제든지 동적으로 변할 수 있습니다. 이러한 특징을 동적 타이핑(dynamic typing)이라 하며, 자바스크립트를 정적 타입 언어와 구별하기 위해 동적 타입 언어라고 합니다.
대표적인 언어로는 Javascript, Python, PHP, Ruby, Lisp 등이 있습니다.

<u>정적 타입 언어는 변수 선언 시점에 변수의 타입이 결정되고 변수의 타입을 변경할 수 없습니다. 자바스크립트에서는 값을 할당하는 시점에 변수의 타입이 동적으로 결정되고 변수의 타입을 언제든지 자유롭게 변경할 수 있습니다.</u>
