# Week 1-1. Welcome to JavaScript

생성일: June 9, 2024 2:46 AM

**<목차>**

spectacular 하고 magnificent 한 프론트엔드의 세계에 첫 발을 떼신 여러분 모두 반갑습니다. 이 챕터에서는 앞으로 공부하실 JavaScript가 어떤 프로그래밍 언어인지 알아보고, JavaScript 기초 문법을 함께 배워보고자 합니다. 그럼 출발해보자구요🏃

![javameme1.webp](Week%201-1%20Welcome%20to%20JavaScript%209bf4ecb3baff428f86edfedaec42dd30/javameme1.webp)

## 프로그래밍이란 뭐라고 생각하나요?

**프로그래밍**이란 컴퓨터에게 실행을 요구하는 일종의 커뮤니케이션입니다. 0과 1밖에 알지 못하는 기계가 실행할 수 있을 정도로 정확하고 상세하게 요구를 설명하는 작업이며, 그 결과물이 바로 **코드**인 것입니다.

## 컴파일러는 뭐고 인터프리터는 뭔가요?

우리가 코드를 통해 내린 명령을 수행할 주체는 컴퓨터입니다. 따라서 사람이 이해할 수 있는 자연어가 아니라 컴퓨터가 이해할 수 있는 언어, 즉 기계어로 명령을 전달해야 하죠.

기계어는 우리가 사용하는 언어와는 너무나도 체계가 다르기 때문에 사람이 기계어로 직접 명령을 전달하는 것은 매우 어렵습니다. 기계어로 직접 명령을 전달하는 것을 대신할 가장 유용한 대안은 사람이 이해할 수 있는 약속된 구문으로 구성된 프로그래밍 언어를 사용해 프로그램을 작성한 후, 그것을 컴퓨터가 이해할 수 있는 기계어로 변환하는 일종의 번역기를 이용하는 것입니다.

이 일종의 번역기를 **컴파일러(compiler)** 혹은 **인터프리터(interpreter)**라고 부릅니다.

![스크린샷 2023-04-10 오후 2.55.24.png](Week%201-1%20Welcome%20to%20JavaScript%209bf4ecb3baff428f86edfedaec42dd30/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-10_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_2.55.24.png)

## **JavaScript 는 뭔가요?**

JavaScript는 90년대부터 주로 웹 브라우저 상에서 UI 를 동적으로 보여주기 위하여 사용되어온 프로그래밍 언어입니다. 기존에는 브라우저에서만 사용해왔던 언어인데, 이제는 단순히 웹페이지에서만 국한되지 않고 Node.js 런타임을 통하여 서버 쪽에서도 사용을 할 수 있게 되었습니다. 

그리고 하드웨어에서도 Node.js 를 통하여 JavaScript 를 사용 할 수 있기 때문에 IoT(사물인터넷) 진영에서도 사용 될 수도 있죠.

또한 JavaScript는 별도의 컴파일 작업을 수행하지 않는 인터프리터 언어입니다.  인터프리터는 소스코드를 즉시 실행하고 컴파일러는 빠르게 동작하는 머신 코드를 생성하고 최적화합니다. 이를 통해 컴파일 단계에서 추가적인 시간이 필요함에도 더욱 빠르게 코드를 실행할 수 있습니다. 하지만 자바스크립트는 런타임에 컴파일되며 실행 파일이 생성되지 않고 인터프리터의 도움 없이 실행할 수 없기 때문에 컴파일러 언어라고 할 수는 없습니다.

자바스크립트는 여러분의 브라우저에서 언제든지 사용 할 수 있습니다. 만약 현재 여러분이 크롬브라우저가 아닌 다른 브라우저를 사용중이라면 크롬을 설치하여 실행해보세요. 그리고 개발자 도구를 열어보세요.

개발자 도구는 윈도우 Ctrl + Shift + I 또는 macOS Command + Option + I 키를 눌러서 열 수 있습니다.

크롬 개발자 도구에서 Console 탭을 열고 입력창에 다음 코드를 입력해보세요.

```jsx
console.log('Hello JavaScript!');
```

![https://i.imgur.com/xA2b56x.png](https://i.imgur.com/xA2b56x.png)

위 이미지와 같이 Hello JavaScript! 가 보여졌나요?

여기서 `console.log` 는 콘솔에 특정 내용을 출력하라는 것을 의미합니다.

이번에는 조금 다른걸 해볼까요?

다음 코드를 한번 입력해보세요.

```jsx
console.log(1 + 2 + 3 + 4);
```

10 이라는 결과물이 나타났나요?

우리는 이렇게 JavaScript 를 통하여 연산을 할 수도 있답니다.

그런데 아무래도 매번 코드를 작성 할 때마다 크롬 개발자 도구에서 하는 것은 조금 불편합니다.

그래서, 여러분께 유용한 웹사이트를 소개드려볼까 합니다(알면 말어잉 ~..)

바로 [CodeSandbox](https://codesandbox.io/) 이라는 사이트인데요, 코드를 작성하고 바로 결과물을 확인 할 수 있는 서비스입니다.

위 링크를 열고 Github 계정으로 로그인 하시면 이러한 화면이 나타날 겁니다.

![스크린샷 2023-02-24 오후 3.00.45.png](Week%201-1%20Welcome%20to%20JavaScript%209bf4ecb3baff428f86edfedaec42dd30/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-02-24_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_3.00.45.png)

우측 상단의 Create를 누르시고 Vanilla 를 선택하세요. Vanilla 는 다른 라이브러리 없이 자바스크립트만 사용하겠다는 의미입니다.

![스크린샷 2023-02-24 오후 3.02.19.png](Week%201-1%20Welcome%20to%20JavaScript%209bf4ecb3baff428f86edfedaec42dd30/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-02-24_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_3.02.19.png)

다음과 같은 에디터가 나타날텐데, 상단에 Fork 버튼을 누르세요.

![https://i.imgur.com/QcpNUR9.png](https://i.imgur.com/QcpNUR9.png)

그 다음,

index.js 파일의 내용을 다 지우고 다음 코드를 입력해보세요.

```jsx
console.log('안녕하세요!');
console.log('JavaScript 를 배워봅시다');
```

그 다음에 우측의 Console 을 누르시면 결과물이 나타납니다.

![https://i.imgur.com/QPqvmW8.png](https://i.imgur.com/QPqvmW8.png)

흰 페이지는 HTML 결과물을 보여주는 곳인데, 지금은 필요 없으니 이렇게 Console 창을 드래그하여 위로 쭉 끌어 올려주세요.

![https://i.imgur.com/g3NRbuj.gif](https://i.imgur.com/g3NRbuj.gif)

또는 이렇게 할 수도 있습니다.

![https://i.imgur.com/TAjKRUv.gif](https://i.imgur.com/TAjKRUv.gif)

이렇게 콘솔 탭을 옮기고 나서 다시 자바스크립트를 실행하려면, 코드에 변화를 주어야 합니다 (위 화면에서는 JavaScript 를 배워봅시다 뒤에 느낌표를 찍었습니다.)

**이제 여러분은 JavaScript 를 작성하고, 실행 할 준비가 되었습니다! ✅**

하지만 작성과 실행을 할 수 있다고 코딩이 가능해 지는건 아니겠죠😅

그래서 JavaScript를 다루기 위한 기본적인 문법들을 다뤄보고자 합니다.

이 내용들은 앞서 공부해보신 다른 언어와 닮은 부분도 많을 것입니다. 어떤 부분이 같고, 어떤 부분을 다르게 표현하는지 비교하면서 따라와주세요😉

========================================================================

## 01**.  변수와 상수 그리고 데이터 타입**

우선 변수와 상수에 대해서 알아봅시다. 변수와 상수는, 특정 이름에 특정 값을 담을 때 사용합니다.

예를 들어서 우리가 value 라는 이름에 1 이라는 값을 넣는다고 가정해봅시다.

그러면, 코드를 이렇게 입력하면 됩니다.

```jsx
let value = 1;
```

그러면, 앞으로 우리가 value 를 조회하면 value 는 1을 가르키게 됩니다. 예를 들어서 우리가 이전에 배웠던 console.log 를 통하여 value 값을 출력하도록 해보세요.

```jsx
let value = 1;
console.log(value);
```

![https://i.imgur.com/BMkIXLN.png](https://i.imgur.com/BMkIXLN.png)

1이라는 값이 우측에 나타날 것입니다.

특정 이름에 특정 값을 설정하는 것. 우리는 이것을 **선언** 이라고 부릅니다. 쉽게 말하면 이제부터 value 는 1이야~ 라고 정해주는 것이죠.

값을 선언 할 때에는 두가지 종류가 있는데요, 하나는 변수이고, 하나는 상수입니다.

### **변수**

변수는, **바뀔수 있는 값**을 말합니다. 한번 값을 선언하고 나서 바꿀 수 있습니다.

```jsx
let value = 1;
console.log(value);
value = 2;
console.log(value);
```

![https://i.imgur.com/s3f8oyZ.png](https://i.imgur.com/s3f8oyZ.png)

변수를 선언 할 때에는 이렇게 `let` 이라는 키워드를 사용합니다. 사용 하실 때 주의 할 점은 한번 선언했으면 똑같은 이름으로 선언하지 못합니다.

이런 코드는 오류가 발생합니다.

```jsx
let value = 1;
let value = 2;
```

![https://i.imgur.com/Zy4rXMV.png](https://i.imgur.com/Zy4rXMV.png)

### **상수**

상수는, **한번 선언하고 값이 바뀌지 않는 값**을 의미합니다. 즉, 값이 고정적이죠. 상수를 선언 할 때에는 다음과 같이 선언합니다.

```jsx
const a = 1;
```

이렇게, 상수를 선언 할 때에는 `const` 키워드를 사용합니다. 상수를 선언하고 나면, 값을 바꿀 수 없습니다.

한번 다음 코드를 입력해보세요.

```jsx
const a = 1;
a = 2;
```

![https://i.imgur.com/mlqPNuh.png](https://i.imgur.com/mlqPNuh.png)

"Error: "a" is read-only" 라는 오류가 발생했습니다. 한번 상수로 선언했으면 값을 바꿀 수 없음을 의미합니다.

상수를 선언할 때에도 마찬가지로 한번 선언했으면 같은 이름으로 선언 할 수 없습니다.

```jsx
const a = 1;
const a = 2;
```

![https://i.imgur.com/uvXKCHr.png](https://i.imgur.com/uvXKCHr.png)

### **데이터 타입**

우리가 변수나 상수를 선언하게 될 때, 숫자 외에도 다른 값들을 선언 할 수 있습니다. 종류는 굉장히 많은데요 그 중에서 가장 기본적인 것들을 알아보겠습니다.

### 숫자 (Number)

우선, 이미 사용해보았지만, 숫자는 그냥 바로 값을 대입하면 됩니다.

```jsx
let value = 1;
```

### **문자열 (String)**

그리고, 텍스트 (주로, 프로그래밍 언어에서는 이를 문자열이라고 부릅니다.) 형태의 값은 작은 따옴표 혹은 큰 따옴표로 감싸서 선언합니다.

```jsx
let text = 'hello';
let name = "좌봐스크립트";
```

### **참/거짓 (Boolean)**

이번에는 boolean 이라는 것에 대해서 알아보겠습니다. boolean 은, 참 혹은 거짓 두가지 종류의 값만을 나타낼 수 있습니다.

```jsx
let good = true;
let loading = false;
```

참은 true, 거짓은 false 입니다.

### **null 과 undefined**

자바스크립트에서는 "없음" 을 의미하는 데이터 타입이 두 종류가 있는데요, 하나는 `null` 이고 하나는 `undefined` 인데, 둘의 용도가 살짝 다릅니다.

null 은 주로, 이 값이 없다! 라고 선언을 할 때 사용합니다.

```jsx
const friend = null;
```

반면, undefined 는, 아직 값이 설정되지 않은 것을 의미합니다.

다음 코드를 입력해보세요.

```jsx
let criminal;
console.log(criminal);
```

criminal 이라는 변수를 선언하긴 했지만 값을 지정해주지는 않았습니다. 이를 console.log 를 통해 보여주도록 하면 undefined 라는 값이 나타나게 됩니다.

![https://i.imgur.com/bJCIYsx.png](https://i.imgur.com/bJCIYsx.png)

null 과 undefined 는 둘 다 값이 없음을 의미하는건 맞는데, **null 은 우리가 없다고, 고의적으로 설정하는 값을 의미하고, undefined 는 우리가 설정을 하지 않았기 때문에 없는 값을 의미합니다.**

## **02. 연산자**

**연산자**는 프로그래밍 언어에서 특정 연산을 하도록 하는 문자입니다.

예를 들어서, 우리가 변수와 상수를 배울 때 다음과 같은 코드를 작성했었지요?

```jsx
let value = 1; // 변수 선언
value = 2; // 대입 연산자
```

여기서 두번째 줄에서 사용된 `=` 문자가 바로 연산자입니다. 연산자의 종류는 굉장히 많습니다. 그 중에서 `=` 는, 대입 연산자에 해당합니다. 첫번째 줄은 새로운 변수를 선언하는 것으로서, 대입 연산자에 해당하지 않습니다.

### **산술 연산자**

산술 연산자는 사칙연산과 같은 작업을 하는 연산자를 의미합니다.

- `+`: 덧셈
- `-`: 뺼셈
- `*`: 곱셈
- `/`: 나눗셈

위 4가지가 가장 기본적인 산술 연산자입니다. 이 외에도 몇가지가 더 있는데요, 먼저 위 연산자들을 한번 사용해봅시다.

```jsx
let a = 1 + 2;
console.log(a);
```

위 코드는 a 값을 선언 할 때 1 + 2 의 결과물을 담습니다. 따라서 콘솔에선 3 이라는 숫자가 나타나겠죠.

![https://i.imgur.com/qk9W5NT.png](https://i.imgur.com/qk9W5NT.png)

```jsx
let a = 1 + 2 - (3 * 4) / 4;
console.log(a);
```

이렇게 우리가 계산기를 두드릴 때 처럼 할 수도 있습니다.

![https://i.imgur.com/Vn7xxWa.png](https://i.imgur.com/Vn7xxWa.png)

그리고, 이런 것도 할 수 있습니다. 이 또한 산술 연산자의 일부입니다.

```jsx
let a = 1;
a++;
++a;
console.log(a);
```

결과는 3이 나타납니다. `++` 는 특정 변수에 1을 바로 더해줍니다. 그런데, ++ 가 변수 이름 앞에 오는 것과 뒤에 오는것에 차이가 있습니다.

```jsx
let a = 1;
console.log(a++);
console.log(++a);
```

![https://i.imgur.com/mfzGBCy.png](https://i.imgur.com/mfzGBCy.png)

`console.log(a++);` 를 할 때에는 1을 더하기 직전 값을 보여주고 `console.log(++a);` 를 할 때에는 1을 더한 다음의 값을 보여준다는 차이가 있습니다.

덧셈 외에도 뺄셈도 똑같이 할 수 있습니다.

```jsx
let a = 1;
a--;
console.log(a);
```

결과는 0이 나타나게 됩니다.

### **대입 연산자**

대입 연산자는 특정 값에 연산을 한 값을 바로 설정 할 때 사용 할 수 있는 연산자입니다. 예를 들어서 다음과 같은 코드가 있다면

```jsx
let a = 1;
a = a + 3;
```

위 코드를 대입 연산자를 사용하면 다음과 같이 작성할 수 있습니다.

```jsx
let a = 1;
a += 3;
```

덧셈 말고 다른 연산도 가능합니다.

```jsx
let a = 1;
a += 3;
a -= 3;
a *= 3;
a /= 3;
console.log(a);
```

결과는 1이 나타나게 됩니다.

### **논리 연산자**

논리 연산자는, 불리언 타입 (true 혹은 false)를 위한 연산자입니다. 논리 연산자는 다음 장에서 우리가 if 문을 배울 때 매우 유용합니다.

총 3가지가 있습니다.

- `!`: NOT
- `&&`: AND
- `||`: OR

OR의 경우엔 엔터키 위의 \ 문자를 Shift 누른 상태로 누르면 됩니다.

### **NOT**

NOT 연산자는 true 는 false 로, false 는 true 로 바꿔줍니다.

```jsx
const a = !true;
console.log(a);
```

a 값은 false 입니다.

```jsx
const b = !false;
console.log(b);
```

b 값은 true 가 됩니다.

### **AND**

AND 연산자는 양쪽의 값이 둘 다 true 일때만 결과물이 true 입니다.

```jsx
const a = true && true;
console.log(a);
```

다음과 같은 상황엔 모두 false 입니다.

```jsx
let f = false && false;
f = false && true;
f = true && false;
```

### **OR**

OR 연산자는 양쪽의 값 중 하나라도 true 라면 결과물이 true 입니다. 그리고, 두 값이 둘 다 false 일 때에만 false 입니다.

다음 상황엔 t 값은 true 입니다.

```jsx
let t = true || false;
t = false || true;
t = true || true;
```

반면 상황엔 false 입니다.

```jsx
let f = false || false;
```

### **연산 순서**

사칙연산을 할 때 곱셈 나눗셈이 먼저고 그 다음이 덧셈 뺄셈인 것 처럼, 논리 연산자도 순서가 있습니다. 순서는 NOT -> AND -> OR 입니다. 예를 들어 다음과 같은 코드가 있다고 가정해봅시다.

```jsx
const value = !((true && false) || (true && false) || !false);
```

괄호로 감싸져있을 때에는 가장 마지막에 처리를 하니까 맨 앞 NOT 은 나중에 처리하겠습니다.

우선 NOT 을 처리합니다.

```jsx
!((true && false) || (true && false) || true);
```

그 다음엔 AND 를 처리합니다.

```jsx
!(false || false || true);
```

OR 연산자를 좌측에서 우측 방향으로 처리를 하게 되면서 다음과 같이 처리됩니다.

```jsx
!true;
```

결국 결과값은 false 가 됩니다.

### **비교 연산자**

비교 연산자는 두 값을 비교 할 때 사용 할 수 있습니다.

### **두 값이 일치하는지 확인**

```jsx
const a = 1;
const b = 1;
const equals = a === b;
console.log(equals);
```

`===` 는 두 값이 일치하는지 확인해줍니다. 일치한다면, true, 일치하지 않는다면 false 가 나타납니다. 위 코드의 경우엔 true 가 나타나겠죠?

두 값이 일치 하는지 확인 할 때 `=` 문자를 3번 사용하는데요, 2개로도 비교를 할 수는 있습니다.

```jsx
const a = 1;
const b = 1;
const equals = a == b;
console.log(equals);
```

위 코드는 똑같은 결과 true 를 반환하긴 하는데요, `=` 문자가 3개 있을 때와 2개 있을 떄의 차이점은 2개 있을때에는 타입 검사까지는 하지 않는다는 것입니다.

예를 들어서 `==` 를 사용하면 숫자 1과 문자 '1' 이 동일한 값으로 간주됩니다.

```jsx
const a = 1;
const b = '1';
const equals = a == b;
console.log(equals);
```

결과: true

그리고, 0 과 false 도 같은 값으로 간주되지요.

```jsx
const a = 0;
const b = false;
const equals = a == b;
console.log(equals);
```

결과: true

그리고 undefined 와 null 도 같은 값으로 간주됩니다.

```jsx
const a = null;
const b = undefined;
const equals = a == b;
console.log(equals);
```

결과: true

앞으로 여러분이 두 값이 일치하는지 비교 할 때에는 `==` 대신 `===` 를 사용 할 것을 권장 드립니다. `==` 를 사용하다보면 실수를 할 확률이 높아집니다.

### **두 값이 일치하지 않는지 확인**

두 값이 일치하지 않는지 확인 할 때에는 `!==` 를 사용하면 됩니다.

```jsx
const value = 'a' !== 'b';
```

결과물은 true 가 됩니다.

`!=` 를 사용하게 되면 타입 검사를 하지 않습니다.

```jsx
console.log(1 != '1');
console.log(1 !== '1');
```

처음엔 false, 두번째에서는 true가 나타납니다. 두 값이 일치하지 않는지 확인 할 때에도, !== 를 사용 할 것을 권장드립니다.

### **크고 작음**

두 값 중에서 무엇이 더 크고 작은지 비교하기 위해서는 다음 연산자를 사용 할 수 있습니다.

```jsx
const a = 10;
const b = 15;
const c = 15;

console.log(a < b); // true
console.log(b > a); // true
console.log(b >= c); // true
console.log(a <= c); // true
console.log(b < c); // false;
```

### **문자열 붙이기**

두 문자열을 붙일 때에는 `+` 로 할 수 있습니다.

```jsx
const a = '안녕';
const b = '하세요';
console.log(a + b); // 안녕하세요
```

## **03. 조건문**

조건문을 사용하면 특정 조건이 만족됐을 때 특정 코드를 실행할 수 있습니다.

### **if 문**

가장 기본적인 조건문은 if 문입니다.

if문은, "~~하다면 ~~를 해라" 를 의미합니다.

예시 코드를 한번 봅시다.

```jsx
const a = 1;
if (a + 1 === 2) {
  console.log('a + 1 이 2 입니다.');
}
```

결과는, "a + 1 이 2 입니다." 이 출력됩니다.

하지만, 만약에 여기서 a 를 0 으로 바꾼다면 어떨까요?

```jsx
const a = 0;
if (a + 1 === 2) {
  console.log('a + 1 이 2 입니다.');
}
```

결과는, 아무것도 출력되지 않습니다.

if문을 사용하면, 이렇게 특정 조건이 만족 될 때에만 특정 코드를 실행 시킬 수 있습니다.

```jsx
if (조건) {
  코드;
}
```

조건이 만족됐을 때 실행시킬 코드가 `{ }` 로 감싸져있는데요, 이를 코드 블록이라고 합니다.

만약에 조건이 true 가 된다면 우리가 지정한 코드가 실행되는 것이고, false 가 된다면 코드가 실행되지 않습니다.

### **if-else 문**

if-else문은 "~~하다면 ~~하고, 그렇지 않다면 ~~해라." 를 의미합니다.

예시 코드를 볼까요?

```jsx
const a = 10;
if (a > 15) {
  console.log('a 가 15 큽니다.');
} else {
  console.log('a 가 15보다 크지 않습니다.');
}
```

위 코드의 결과는 다음과 같습니다.

```jsx
"a 가 10보다 크지 않습니다."
```

만약에 특정 조건이 만족할 때와 만족하지 않을 때 서로 다른 코드를 실행해야 된다면 if-else 구문을 사용 할 수 있습니다.

### **if-else if 문**

if-else if 문은 여러 조건에 따라 다른 작업을 해야 할 때 사용합니다.

예시 코드를 따라 적어보세요.

```jsx
const a = 10;
if (a === 5) {
  console.log('5입니다!');
} else if (a === 10) {
  console.log('10입니다!');
} else {
  console.log('5도 아니고 10도 아닙니다.');
}
```

결과는 다음과 같습니다.

```jsx
"10입니다!"
```

한번 a 값을 5로 바꾸고 실행해보고, 7 로 바꾸고 실행해보세요.

```jsx
a = 5 -> "5입니다!"
a = 7 -> "5도 아니고 10도 아닙니다."
```

### **switch/case 문**

switch/case 문은 특정 값이 무엇이냐에 따라 다른 작업을 하고 싶을 때 사용합니다.

다음 예시 코드를 실행해보세요.

```jsx
const device = 'iphone';

switch (device) {
  case 'iphone':
    console.log('아이폰!');
    break;
  case 'ipad':
    console.log('아이패드!');
    break;
  case 'galaxy note':
    console.log('갤럭시 노트!');
    break;
  default:
    console.log('모르겠네요..');
}
```

device 값을 'iphone', 'ipad', 'galaxy note', 'macbook' 으로 순서대로 바꿔가면서 코드를 실행해보세요.

device 값에 따라서 다른 결과가 출력되고 있나요?

switch/case 문은 이와 같이 특정 값이 무엇이냐에 따라 다른 작업을 수행 할 수 있게 해줍니다.

switch/case 문에서는 각 case 에서 실행할 코드를 작성하고 맨 마지막에 `break;` 를 해주어야 합니다. break 를 하지 않으면 그 다음 case 의 코드까지 실행해버립니다.

그리고, 맨 아래의 `default:` 는 device 값이 우리가 case 로 준비하지 않은 값일 경우를 의미합니다.

## **04. 반복문**

반복문은 특정 작업을 반복적으로 할 때 사용할 수 있는 구문입니다.

### **for**

for 문은 가장 기본적인 반복문입니다. 특정 값에 변화를 주어가면서 우리가 정한 조건이 만족된다면 계속 반복합니다.

한번 다음 코드를 따라 적어보세요.

```jsx
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

![https://i.imgur.com/oLVt44l.png](https://i.imgur.com/oLVt44l.png)

결과가 0부터 9까지 잘 나타났나요?

for 문을 다음과 같이 사용합니다.

```jsx
for (초기 구문; 조건 구문; 변화 구문;) {
  코드
}
```

for 문을 사용 할 때 보통 `i++` 를 해서 1씩 증감하는 형태로 사용합니다. 그런데, 1씩 빼는 형태도 가능합니다. 다음 코드를 한번 실행해보세요.

```jsx
for (let i = 10; i > 0; i--) {
  console.log(i);
}
```

![https://i.imgur.com/59mYcGp.png](https://i.imgur.com/59mYcGp.png)

10부터 1까지 결과가 잘 나타났나요?

for 문은 이렇게 숫자에 변화를 주어가면서 반복적으로 작업을 실행합니다.

### **while**

while문은 특정 조건이 참이라면 계속해서 실행하는 반복문입니다. for 문은 특정 숫자를 가지고 숫자의 값을 비교하고, 증감해주면서 반복을 한다면, while문은 조건을 확인만 하면서 반복을 합니다. 때문에, 조건문 내부에서 변화를 직접 주어야 합니다.

우리가 가장 처음 작성했던 0 부터 9 까지 콘솔에 출력을하는 반복문을 while 문으로 구현해보겠습니다.

```jsx
let i = 0;
while (i < 10) {
  console.log(i);
  i++;
}
```

while 문을 사용 할 때에는 조건문이 언젠간 false 가 되도록 신경쓰셔야 합니다. 만약에 언젠간 false 로 전환이 되지 않는다면 반복문이 끝나지 않고 영원히 반복됩니다.

### **break 와 continue**

반복문 안에서는 `break` 와 `continue` 를 통하여 반복문에서 벗어나거나, 그 다음 루프를 돌게끔 할 수 있습니다.

```jsx
for (let i = 0; i < 10; i++) {
  if (i === 2) continue; // 다음 루프를 실행
  console.log(i);
  if (i === 5) break; // 반복문을 끝내기
}
```

i 가 2 일땐 `continue` 를 하여 원래 console.log 를 해야 하지만 그 코드를 수행하지 않고 바로 3으로 넘어갑니다.

i 가 5 일땐 `break` 를하여 반복문을 종료시킵니다.

![https://i.imgur.com/UmWM0tA.png](https://i.imgur.com/UmWM0tA.png)

## **05. 함수**

함수는, 특정 코드를 하나의 명령으로 실행 할 수 있게 해주는 기능입니다.

예를 들어서, 우리가 특정 값들의 합을 구하고 싶을 때는 다음과 같이 코드를 작성합니다.

```jsx
const a = 1;
const b = 2;
const sum = a + b;
```

한번, 이 작업을 함수로 만들어보겠습니다.

```jsx
function add(a, b) {
  return a + b;
}

const sum = add(1, 2);
console.log(sum);
```

결과는 3이 됩니다.

함수를 만들 때는 `function` 키워드를 사용하며, 함수에서 어떤 값을 받아올지 정해주는데 이를 파라미터(매개변수)라고 부릅니다.

함수 내부에서 `return` 키워드를 사용하여 함수의 결과물을 지정 할 수 있습니다.

추가적으로, `return` 을 하게 되면 함수가 끝납니다. 만약 다음과 같이 코드가 작성된다면, return 아래의 코드는 호출이 안됩니다.

```jsx
function add(a, b) {
  return a + b;
  console.log('호출이 되지 않는 코드!');
}

const sum = add(1, 2);
console.log(sum);
```

### **Hello, name!**

name 이라는 파라미터를 넣으면 콘솔에 'Hello name!' 이라는 결과를 출력하는 코드를 작성해봅시다.

```jsx
function hello(name) {
  console.log('Hello, ' + name + '!');
}
hello('meotsa');
```

결과물은 다음과 같습니다.

```jsx
"Hello, meotsa!"
```

console.log 를 하게 될 때 우리는 문자열을 조합하기 위해서 `+` 연산자를 사용했습니다. 이렇게 문자열을 조합 할 때 `+` 를 사용해도 큰 문제는 없지만, 더욱 편하게 조합을 하는 방법이 있습니다. 바로, ES6 의 템플릿 리터럴 (Template Literal)이라는 문법을 사용하는 것 입니다.

> ES6 가 뭔가요?
> 
> 
> ES6 는 ECMAScript6 를 의미하며, 자바스크립트의 버전을 가르킵니다. ES6는 2015년에 도입이 되었습니다. ES6 는 ES2015 라고 불리기도 합니다. 그리고 2015년 이후에 계속해서 새로운 자바스크립트 버전이 나오고 있습니다. ES7(ES2016) ES8(ES2017) ES9(ES2018) ES10(ES2019).. 새로운 자바스크립트 버전이 나올때마다 새로운 문법이 소개됩니다.
> 
> 브라우저 버전에 따라 지원되는 자바스크립트 버전이 다릅니다. 하지만, 보통 웹 개발을 할 때에는 Babel 이라는 도구를 사용하여 최신 버전의 자바스크립트가 구버전의 브라우저에서도 실행되도록 할 수 있습니다. (정확히는, 최신버전 자바스크립트를 구버전 형태로 변환하는 작업을 거칩니다.)
> 

템플릿 리터럴을 사용하여 구현을 해봅시다.

```jsx
function hello(name) {
  console.log(`Hello, ${name}!`); //따옴표가 아닌 백팁
}
hello('velopert');
```

### **화살표 함수**

함수를 선언하는 방식 중 또 다른 방법은 화살표 함수 문법을 사용 하는 것 입니다.

```jsx
const add = (a, b) => {
  return a + b;
};

console.log(add(1, 2));
```

`function` 키워드 대신에 `=>` 문자를 사용해서 함수를 구현했는데요, 화살표의 좌측에는 함수의 파라미터, 화살표의 우측에는 코드 블록이 들어옵니다.

그런데, 만약에 위와 같이 코드 블록 내부에서 바로 return 을 하는 경우는 다음과 같이 줄여서 쓸 수도 있습니다.

```jsx
const add = (a, b) => a + b;
console.log(add(1, 2));
```

아까 만들었던 getGrade 함수처럼 여러 줄로 구성되어있는 경우에는 코드 블록을 만들어야합니다.

```jsx
const getGrade = score => {
  if (score === 100) {
    return 'A+';
  } else if (score >= 90) {
    return 'A';
  } else if (score === 89) {
    return 'B+';
  } else if (score >= 80) {
    return 'B';
  } else if (score === 79) {
    return 'C+';
  } else if (score >= 70) {
    return 'C';
  } else if (score === 69) {
    return 'D+';
  } else if (score >= 60) {
    return 'D';
  } else {
    return 'F';
  }
};
const grade = getGrade(90);
console.log(grade);
```

### **함수의 기본 파라미터**

한번, 우리가 원의 넓이를 구하는 함수를 만들어보겠습니다.

```jsx
function calculateCircleArea(r) {
  return Math.PI * r * r;
}

const area = calculateCircleArea(4);
console.log(area); // 50.26548245743669
```

여기서 Math.PI 는 원주율 파이(π) 값을 가르킵니다.

만약 우리가 이 함수에 r 값을 넣어주지 않으면 어떤 결과가 나타날까요?

```jsx
function calculateCircleArea(r) {
  return Math.PI * r * r;
}

const area = calculateCircleArea();
console.log(area); // NaN
```

결과는 NaN 이 나옵니다. Not a Number 라는 의미로, 우리가 undefined * undefined 이렇게 숫자가 아닌 값에 곱셈을 하니까 이상한 결과물이 나와버렸습니다.

이 함수에서 만약에 r 값이 주어지지 않았다면 기본 값을 1을 사용하도록 설정해봅시다.

```jsx
function calculateCircleArea(r = 1) {
  return Math.PI * r * r;
}

const area = calculateCircleArea();
console.log(area); // 3.141592653589793
```

함수의 기본 파라미터 문법은 화살표 함수에서도 사용 할 수 있습니다.

```jsx
const calculateCircleArea = (r = 1) => Math.PI * r * r;

const area = calculateCircleArea();
console.log(area); // 3.141592653589793
```

이 챕터에서는 JavaScript란 어떤 언어인지 알아보고, 이를 다루기 위해 필요한 기초적인 문법들을 공부해보았습니다. 잠시 숨 고르고 다음 챕터로 넘어가보아요🦥