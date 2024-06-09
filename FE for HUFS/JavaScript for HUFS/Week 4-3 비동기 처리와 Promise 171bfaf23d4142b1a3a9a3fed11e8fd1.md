# Week 4-3. 비동기 처리와 Promise

생성일: June 9, 2024 2:46 AM

이제는 Promise를 비롯해 서버와 직접 통신하는 방법을 배울 차례입니다. 

사실 프론트엔드 개발자를 맨 처음 떠올렸을 때엔 ‘서버와의 통신’보다는 ‘웹페이지 구현’이 우선적으로 떠오르게 마련입니다. 이 글을 쓰는 저 또한 프론트 개발자가 되려 맘 먹었던 계기 역시 ‘디자인적 요소’에 이끌려 선택했던 기억이 떠오릅니다.

엄밀히 따지자면 프론트엔드 개발자는 웹페이지의 디자인을 신경쓰는 직군이 아니라 ‘정제돼있지 않은 데이터들을 정해진 디자인 틀에 맞게 조립하고 동작시키게 하는’ 직군에 가깝습니다. 아마 저 뿐만 아니라 거의 모든 프론트엔드 개발자 지망생이 ‘프론트엔드 개발자는 자기가 원하는 페이지를 만드는 개발자’라는 달콤한 오해(?)를 하며 진입했지 않을까 싶어요.

물론 프론트엔드에서 전혀 디자인적 요소를 다루지 못하는 것은 아닙니다. 토이프로젝트 정도의 로우레벨에서는 디자이너가 없으니 당연히 프론트엔드 개발자가 디자인까지 맡게 되구요, 실무에서도 기술적으로 디자인 반영이 어렵거나 개선시킬 수 있는 지점이 있따면 디자이너와 소통해 기여할 수 있다 합니다. 

하지만! 결론적으로 프론트엔드 개발자의 본분은 디자인보다는 ‘기술적 구현’에 더 가깝다는 점을 인지해주시고 오늘은 그 본분을 다하기 위한 기초 개념들을 배워보도록 하겠습니다 😎

## 왜 서버와 통신할까요?

프론트엔드 개발자라면 서버와 통신하여 가져온 데이터를 화면에 잘 보여줄 수 있어야 합니다. 그런데 그 방법을 배우기 전에 왜 서버와 통신할까요? 한 번 근본적인 질문에 대해 생각해보고 갑시다.

우선 당연하게도 불특정 다수의 로컬 IP에서 우리의 서비스에 접속하고자 요청할 때, 이들에게 서로 다른 페이지를 보여주거나 중앙에서 관리되지 않는 버전이 다른 페이지들을 보여준다면 사용자들은 큰 혼란을 겪게 될 것입니다. 사용자들한테 우리 페이지 파일은 여기 있으니 각자 다운받아서 알아서 쓰도록 해. 라고 말하기보다는 한 곳에 우리가 만든 사이트를 저장해놓고 요청이 들어올 때마다 해당 자원을 전송해주는 편이 훨씬 일관성있겠죠?

![Untitled](Week%204-3%20%E1%84%87%E1%85%B5%E1%84%83%E1%85%A9%E1%86%BC%E1%84%80%E1%85%B5%20%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%E1%84%8B%E1%85%AA%20Promise%20171bfaf23d4142b1a3a9a3fed11e8fd1/Untitled.png)

또한, 유저 입장에서도 데이터를 변경하는 액션(e.g. 블로그 글 쓰기)을 취했을 때 자신이 변경한 데이터가 새로고침 이후에 저장이 안되어 사라지거나 나에게만 보이고 다른 사람에게는 보이지 않는다면 결국 서비스를 쓰지 않을 것입니다. 클라이언트에서 변경하고자 하는 데이터를 한 곳에서 모아 저장하고 변경한다면 매우 쉽게 관리가 가능하고 A가 변경한 데이터를 B에게도 보여줄 수 있겠죠.

결국 이러한 점들이 서버가 왜 필요한지 설명해주는 지점이며 그렇기 때문에 서버와의 연결은 굉장히 중요하다고 이야기할 수 있습니다. 항상 서버와 연결하는게 중요하다는 말은 귀에 피가 나도록 듣는데, 왜 그렇게 사람들이 강조하는지 조금은 이해가 되시나요?

## 그럼 서버와 어떤 방식으로 통신하나요?

서버와 통신하는 이유에 대해 이해했다면, 서버와 구체적으로 어떻게 데이터를 주고 받는지 알아볼 필요가 있습니다.

여기에서 프론트엔드 입문자에게 가장 헷갈리고 와닿지 않는 추상적인 단어가 등장합니다. 바로 ‘API’입니다.

### API

`API`는 **Application Programming Interface**의 준말로써, 서버와 데이터를 주고받는 ‘규칙’ 내지는 ‘포맷’이라고 생각할 수 있습니다.

보통 ‘우리는 카카오 API를 사용해 ~를 만들 것입니다’ 등의 말을 자주 듣곤 하고, 백엔드 개발자와 커뮤니케이션할 때 7할 이상의 대화 내용은 API와 관련된 대화로 ‘혹시 API 나왔나요?’ ‘지금 API에 이 데이터가 빠져있는데…’ 등의 대화를 관찰할 수 있습니다. API 개념을 제대로 이해하지 못한 채 이런 질문을 받으면 많이 괴로우실 겁니다..

![Untitled](Week%204-3%20%E1%84%87%E1%85%B5%E1%84%83%E1%85%A9%E1%86%BC%E1%84%80%E1%85%B5%20%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%E1%84%8B%E1%85%AA%20Promise%20171bfaf23d4142b1a3a9a3fed11e8fd1/Untitled%201.png)

흔히 API를 레스토랑에 빗대어 표현합니다. 손님(내가 만드는 프로그램)이 메뉴판을 보고 웨이터(API)에게 주문을 합니다. 그럼 웨이터는 손님의 주문 내역을 주방(기상청, 공공포탈 등의 서버)에 갖다주고, 요청받은 요리를 완성해 웨이터에게 주면 웨이터가 다시 손님에게 음식을 가져다줍니다. 

![Untitled](Week%204-3%20%E1%84%87%E1%85%B5%E1%84%83%E1%85%A9%E1%86%BC%E1%84%80%E1%85%B5%20%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%E1%84%8B%E1%85%AA%20Promise%20171bfaf23d4142b1a3a9a3fed11e8fd1/Untitled%202.png)

여기서 손님이 프론트엔드 개발자, 주방장이 백엔드 개발자라고 생각한다면 메뉴판이 API가 되는 것입니다. 만약 정해진 메뉴판이 없이 손님이 주방에 직접 와서 음식을 주문해야한다고 하면, 손님마다 원하는 음식의 양도 다를 것이며 재료의 상태, 종류도 가지각색으로 달라질 수 있기 때문에 주방에서 절대 음식을 뺄 수 없는 상황이 될 것입니다. 때문에 메뉴판과 같은 정해져있는 포맷을 보고 주문하고 음식을 받아볼 수 있는 것이며 메뉴판이란 매개체가 있기 때문에 서로가 어떻게 일을 처리하는지 알 필요 없이 메뉴판을 통해 서로를 신뢰할 수 있게 되는 것이죠!

![Untitled](Week%204-3%20%E1%84%87%E1%85%B5%E1%84%83%E1%85%A9%E1%86%BC%E1%84%80%E1%85%B5%20%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%E1%84%8B%E1%85%AA%20Promise%20171bfaf23d4142b1a3a9a3fed11e8fd1/Untitled%203.png)

그래서 프로젝트 개발을 시작하게 되면 맨처음 하는 일은 API 설계와 시스템 구조 설계입니다. 백엔드 개발자들만 이 일을 하는게 아니라 프론트엔드 개발자도 참여하여 각 페이지마다 어떤 데이터가 필요하고 언제 필요한지 서로 알 수 있게 설계하는 과정을 거쳐야 합니다.

## AJAX란?

자, 지금까지 서버와 통신해야하는 이유에 대해 이해했습니다. 이제부터는 구체적인 방법들을 살펴볼탠데요, 4-1 챕터에서 `MPA`와 `SPA`에 대해 배웠던 기억을 되살려볼까요?

`MPA`는 웹페이지에 변경사항이 생길 때마다 페이지 전체를 서버로부터 받아오는 방법론을 의미했고, `SPA`는 필요한 부분만 부분적으로 데이터를 받아와 클라이언트 레벨에서 최신화하는 방법론을 뜻했죠? 그렇다면 어떻게 `MPA`에서 `SPA`로 넘어오게 되었을까요?

### AJAX의 등장배경

바로 `AJAX`란 비동기 기법을 사용해 진화할 수 있었습니다. `AJAX`는 **Asynchronous JavaScript and XML**의 약자로, 말그대로 자바스크립트와 XML을 이용한 비동기적 정보 교환 기법을 의미합니다. 사실 `AJAX`는 1999년 3월에 정립된 개념이라고 합니다. 마이크로소프트의 IE5 독자 규격을 통해 발표가 됐는데, 당시에는 브라우저 공통 스펙이 아니라 윈도우 한정 비표준 기술로서 개념적으로는 괜찮은 접근이었지만 동적인 페이지 렌더링의 수요가 없었다는 점, `AJAX` 방식이 무거운 기술이라는 점에서 빛을 보지 못했습니다.

그러다가 2005년 구글이 ‘구글맵스’ 웹앱을 `AJAX`로만 구현하면서 화제가 되었고 그 때부터 웹의 발전(정확히는 웹앱 프로그래밍 언어로서의 자바스크립트에 대한 가능성)과 함께 `AJAX`가 주류 기술로 채택되기 시작했습니다.

### AJAX의 동작원리 : XMLHttpRequest

원래 `AJAX`는 이름에서 표기한 것처럼 **XML**이란 녀석을 활용하는데요, XML을 구글링해보면 아래와 같은 정의를 살펴볼 수 있습니다.

**`XML**(Extensible Markup Language)은 W3C에서 개발된, 다른 특수한 목적을 갖는 마크업 언어를 만드는데 사용하도록 권장하는 다목적 마크업 언어이다.`

XML에 대해 자세히 알 필요 없습니다. 그냥 웹 확장성을 갖춘 HTML 개량 언어라고 생각하셔도 무방합니다. 네트워크 통신 시에 잘 정리돼있는 XML을 포맷으로 데이터를 주고받는다 생각하시고, 저희가 주목할 것은 브라우저에서 제공하는 Web API인 `XMLHttpRequest`라는 녀석입니다. 

`AJAX`는 원래 `XMLHttpRequest` 객체를 기반으로 동작합니다. 예시를 봐볼까요?

```jsx
// XMLHttpRequest 객체 생성
const xhr = new XMLHttpRequest();

// HTTP 요청 초기화
xhr.open('GET', 'https://jsonplaceholder.typicode.com/todos/1')

// HTTP 요청 전송
xhr.send();

// HTTP 응답 처리
xhr.onreadystatechange = () => {
	if (xhr.readyState !== XMLHttpRequest.DONE) return;
	if (xhr.status === 200) {
		console.log(JSON.parse(xhr.response));
	} else {
		console.error('Error', xhr.status, xhr.statusText);
	}
};
```

위는 `XMLHttpRequest` 메소드를 이용한 원론적인 `AJAX` 통신 방법(바닐라 자바스크립트)입니다. 메소드들을 일일이 호출해야해서 매우 귀찮죠? 다행히 이런 원론적인 기법을 보완하여 `fetch()` API나 axios같은 유명한 라이브러리가 있으며 `XMLHttpRequest`를 직접 사용할 일은 없습니다. 그리고 요새는 XML보다 **JSON** 포맷을 거의 모든 곳에서 쓰고 있어서 ‘AJAX의 원리는 XML형태의 데이터를 주고받는 방식이구나~’ 정도로만 알고만 가면 되겠습니다 ☺️

잠깐, JAX는 뭔지 알았는데 **Asychronous**는 무슨 뜻인가요? 비동기적인? 비동기라는 단어는 2주차 세션에서 들어본 적 있지 않았나요? 그 비동기에 대해 좀 더 자세히 알아봅시다.

## 비동기 처리 방식

‘동기’와 ‘비동기’의 차이는 무엇인가요? ‘동기’적으로 동작한다는 말의 뜻은, 일련의 task들이 서로의 존재를 인지하며 순서를 지킨 채 동작한다는 뜻입니다. ‘비동기’적으로 동작한다는 말은 반대로 task들이 서로를 인식하지 못하고 제각각 동작하는거겠죠. 

2주차에 이벤트 루프를 배우며 예로 들었던 `setTimeout()` 메소드를 다시 가져와봅시다. 

```jsx
function main(){
  console.log('First');
  setTimeout(
    function display(){ console.log('Second'); }
  ,0);
	console.log('Third');
}
main();

//	First
//	Third
//  Second
```

우리의 예상과 달리 `Second`가 마지막에 출력되었을 때의 과정은 어땠나요? `setTimeout` 메소드가 콜 스택에 쌓였다가 timer Web API를 호출하고 제거됐고, `main` 함수가 종료된 이후에야 테스크 큐에 남아있던 `setTimeout` 콜백 함수가 콜 스택으로 호출되어 실행되었죠?

![모든 테스크가 동기적 또는 비동기적으로 작동하는 경우.](Week%204-3%20%E1%84%87%E1%85%B5%E1%84%83%E1%85%A9%E1%86%BC%E1%84%80%E1%85%B5%20%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%E1%84%8B%E1%85%AA%20Promise%20171bfaf23d4142b1a3a9a3fed11e8fd1/Untitled%204.png)

모든 테스크가 동기적 또는 비동기적으로 작동하는 경우.

브라우저에서의 비동기 프로그래밍은 주로 **통신**과 같이 오래 걸리는 작업들을 브라우저에 위임할 때 이루어집니다(2주차에 배웠던 Web API를 생각해보세요 - DOM, AJAX, setTimeout). 만약 setTimeout 메소드같이 시간이 오래 걸리는 일이 실제 서버와의 데이터 통신이라고 생각한다면, 이 과정이 모두 동기적으로만 진행됐을 때 어떤 일이 벌어질까요?

테스트코드에선 아마 `First` → `Second` → `Third` 같은 결과가 나올 것이고 `First` 출력 이후 `Second`가 출력될 때까지 4초 정도의 break가 발생하게 될 것입니다. 

실제 웹페이지에서 동기적으로 실행됐을 때의 결과물은 만약 페이지에서 자바스크립트로 이루어진 블럭이 존재한다면 군데군데 구멍이 뚫린 채로 온전하지 못한 페이지를 사용자가 경험하게 되며 각 구멍이 순서를 지켜가며 채워지므로 완전한 페이지를 보기까지 시간이 소요될 것입니다. 무엇보다도 부드러운 사용자 경험(UX)을 추구하는 프론트엔드 사이드에서는 너무나도 치명적인 단점이겠죠..

이처럼 어떤 일이 완료되기를 기다리지 않고 다음 코드를 실행해 나가는 프로그래밍 방식을 일러 **비동기 프로그래밍(asynchronous programming)**이라고 합니다. 반대로 어떤 일이 완료될 때까지 코드의 실행을 멈추고 기다리는 프로그래밍 방식을 **동기식 프로그래밍(synchronous programming)**이라고 부릅니다.

## 비동기 처리의 시초 : 콜백 함수

가장 기초적인 비동기 프로그래밍은 콜백함수로 만들 수 있습니다. 콜백(Callback)은 다른 함수의 인수로 넘기는 함수를 말하는데, 독자적으로 함수들이 각자의 타이밍에 실행되는 것이 아니라 이전 함수의 실행이 시작되어야만 자신도 실행될 수 있기 때문에 이러한 시간차를 이용해 비동기 데이터 흐름을 제어할 수 있는 것이죠.

### 간단한 콜백 함수 예시

예를 들어서, `<script>` 태그를 만들고 페이지에 태그를 추가한 뒤 스크립트에 추가적인 수정을 해야하는 업무가 주어졌다고 생각해봅시다.

```jsx
function loadScript(src) {
  // <script> 태그를 만들고 페이지에 태그를 추가합니다.
  // 태그가 페이지에 추가되면 src에 있는 스크립트를 로딩하고 실행합니다.
  let script = document.createElement('script');
  script.src = src;
  document.head.append(script);
}
```

함수 `loadScript(src)`는 `<script src="…">`를 동적으로 만들고 이를 문서에 추가합니다. 브라우저는 자동으로 태그에 있는 스크립트를 불러오고, 로딩이 완료되면 스크립트를 실행합니다.

`loadScript` 함수를 불러온 뒤 수정하는 코드를 달기 위해서 아래와 같이 실행할 수 있겠죠.

```jsx
loadScript('/my/script.js'); // script.js엔 "function newFunction() {…}"이 있습니다.

newFunction(); // 함수가 존재하지 않는다는 에러가 발생합니다!
```

이렇게 실행하면 에러를 마주칠거에요. `newFunction`은 `script.js` 파일 안에 위치해있는데, `loadScript` 함수가 실행이 모두 끝난 뒤에 `newFunction`이 호출되지 않고 비동기적으로 호출되기 때문이죠. 자바스크립트는 기본적으로 시간이 오래 걸리는 작업들은 모두 비동기적으로 동작하도록 짜여져있기 때문에 프로그래머가 어떤 함수의 실행 이후 조건부적으로 그 다음 동작을 수행시키고 싶다할 때엔 반드시 비동기 프로그래밍을 해야합니다!

```jsx
function loadScript(src, **callback**) {
  let script = document.createElement('script');
  script.src = src;

  **script.onload = () => callback(script);**

  document.head.append(script);
} 
```

`loadScript` 함수의 두 번째 인수로 스크립트 로딩 후 실행될 함수의 자리를 위처럼 만들어줍시다.

그러면 이제부터는 아래와 같이 작성한다면 원하는 함수를 콜백함수로서 동작시킬 수 있게됩니다.

```jsx
loadScript('/my/script.js', **function() {**
  // 이름 짓지 않은(익명) 콜백 함수를 두 번째 인자로 넘겨주었습니다.
  **newFunction();** // loadScript 함수 안에 콜백 함수의 존재를 알렸으니 이제 함수가 제대로 동작합니다.
 **** ...
**}**); 
```

### 콜백지옥

이 때, 스크립트가 어려 개 있다고 생각해봅시다. 여러 개의 스크립트를 순차적으로 불러오고 싶다면 아래와 같이 코드를 작성해볼 수 있겠죠?

```jsx
loadScript('1.js', function(error, script) {
  if (error) {
    handleError(error);
  } else {
    // ...
    loadScript('2.js', function(error, script) {
      if (error) {
        handleError(error);
      } else {
        // ...
        loadScript('3.js', function(error, script) {
          if (error) {
            handleError(error);
          } else {
            // 모든 스크립트가 로딩된 후, 실행 흐름이 이어집니다. (*)
          }
        });
      }
    })
  }
});
```

조건문으로 에러 핸들링까지 한 비동기 처리 코드입니다. 이 코드를 보면 어떤 생각이 드시나요?

우선 읽기가 너무 불편합니다. 해당 예시는 같은 패턴의 코드를 복붙한거기 때문에 가독성이 그다지 낮지 않지만, 실제로는 각기 다른 함수가 꼬리에 꼬리를 무는 형태가 되기 십상입니다. 각각의 함수도 그 내용이 굉장히 복잡할 것을 예상하면, 콜백 함수로만 비동기를 처리하는 것은 미련한 짓일 거에요..

이런 코딩 패턴을 `콜백 지옥(callback hell)` 또는 `멸망의 피라미드(pyramid of doom)`라고 일컫습니다.

![Untitled](Week%204-3%20%E1%84%87%E1%85%B5%E1%84%83%E1%85%A9%E1%86%BC%E1%84%80%E1%85%B5%20%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%E1%84%8B%E1%85%AA%20Promise%20171bfaf23d4142b1a3a9a3fed11e8fd1/Untitled%205.png)

이런 코딩 패턴으로만 비동기를 처리하는데 많은 불편함이 있었기 때문에, 아예 비동기 처리를 상태로 관리해주는 객체를 제공하는 라이브러리들이 생겨났고 결국 해당 객체가 표준화되어 ES2015에 공식 문법으로 지원되기 시작했으니 그 객체를 `Promise`라 부르게 되었습니다.

## 비동기 처리의 스탠다드 : Promise

### Promise의 뜻

Promise 객체 자체가 낯선 분들이 계실 수 있습니다. 이 글을 쓰는 제게도 제대로 이해하기 전까지 너무나 추상적이고 두려운 존재였습니다. Promise 객체를 왜 약속을 뜻하는 프로미스로 지었을까요?

> A **`Promise`** is a **proxy** for a value not necessarily known when the promise is created. It allows you to associate handlers with an asynchronous action's eventual success value or failure reason. This lets asynchronous methods return values like synchronous methods: **instead of immediately returning the final value, the asynchronous method returns a *promise* to supply the value at some point in the future.** - MDN 공식 문서
> 

위 글은 Promise에 대한 MDN 자바스크립트 공식 문서 중 Promise에 대한 정의입니다. 마지막 문장이 핵심인데요, 이 Promise 란 객체는 아직 확정되지 않은 결과에 대한 임시 상태를 미리 제공하고, 해당 동작이 마무리되어 결과가 나왔을 때 그것을 제공하겠다는 ‘약속’을 해주는 장치입니다.

### Promise의 3가지 상태

임시 상태는 아래와 같이 3가지의 상태가 있는데요,

- Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태
- Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
- Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태

`new Promise()`로 생성된 프로미스가 종료될 때까지 가질 수 있는 상태들입니다.

 `new Promise()` 메소드를 호출하면 Promise가 생성되는데요, 호출 직후엔 Pending 상태가 됩니다.

```jsx
const getData = new Promise((resolve, reject) => {
	$.get('아무 주소', (response) => { // jQuery 문법입니다. 그냥 넘어가셔도 됩니다 :)
		if (response) {
			resolve(response);
		}
		reject(new Error("Request failed"));
	});
});
```

또한 인자에 콜백 함수를 선언할 수 있고, 콜백 함수의 인자는 `resolve`와 `reject`를 넣어줄 수 있습니다. 만약 `get(’아무주소’)` 메소드가 ‘아무 주소’로부터 적절한 응답 값을 가져왔다면 `resolve()` 메소드를 호출할 것이고, 응답이 없으면 `reject()`를 호출하게 됩니다.

![Untitled](Week%204-3%20%E1%84%87%E1%85%B5%E1%84%83%E1%85%A9%E1%86%BC%E1%84%80%E1%85%B5%20%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%E1%84%8B%E1%85%AA%20Promise%20171bfaf23d4142b1a3a9a3fed11e8fd1/Untitled%206.png)

복잡한 설명 필요 없이 통신에 성공했다면(Fulfilled) `resolve()` 메소드가 동작하게 되고, 통신에 실패했다면(Rejected) `reject()` 메소드가 동작하게 됩니다. 별거 없죠?

### then, catch, finally

Promise 의 동작이 모두 끝나고 결과를 반환하면 정상적인 response든 error든 `.then()` 메소드나 `.catch()` 메소드를 통해 핸들링할 수 있습니다.

우선 `.then()` 메소드를 살펴봅시다. 가장 기본이 되는 문법이며 가장 많이 쓰는 문법입니다. `.then()` 은 Promise가 fulfilled 되었을 때 동작하는 메소드이고 그렇다면 `catch`는 자연스럽게 rejected 되었을 때 그 에러를 ‘캐치’한다고 생각하시면 쉬울 거에요.

```jsx
getData.then(
	result => alert(result) // function(result) {alert(result)} 와 같은 문법입니다.
	error => alert(error) // .then()은 완벽하게 에러를 핸들링하지 못합니다(알려주는 정도만 가능하죠).
).catch(err => {
	console.log(err) // 에러 상황을 핸들링하고 싶다면 .catch()로 컨트롤하는 것이 바람직합니다.
})
```

위 코드는 자주 볼 수 있는 코딩 패턴입니다. 어떤 변수에 비동기 통신 프로세스를 할당시키고, 반환하는 Promise 객체에 대해 `.then()` 또는 `.catch()` 메소드를 붙여줘 후속 상황을 핸들링합니다. 이것만 아셔도 Promise는 사실상 다 알고 있다고 말해도 무방해요.

그러나 `.finally()`가 남았습니다. finally? 마지막으로? 도대체 왜 finally란 이름이 붙은 걸까요?

`.finally()` 메소드는 Promise의 최종 상태와 무관하게 처리가 끝났는지 여부를 판별하는 메소드입니다. 

`.then()`이 ‘처리가 끝나고 - 성공했을 때’의 경우이며 

`.catch()`가 ‘처리가 끝나고 - 실패했을 때’의 경우라면, 

`.finally()` 메소드는 처리 자체가 끝났을 때 이행 여부와 관계없이 공통적으로 수행해줘야 할 후처리가 있을 때 사용하면 좋은 메소드입니다.

따라서 아래와 같이 `.then()`이나 `.catch()`보다 먼저 사용하게 됩니다.

```jsx
new Promise((resolve, reject) => {
  ...
}).finally(() => alert("프라미스가 준비되었습니다."))
	.then(result => alert(result))
  .catch(err => alert(err));
```

근데 사실 finally는 자주 쓰이지 않습니다. 그리고 Promise 자체를 자주 쓴다기보다는 Promise를 녹여낸 서드파티 라이브러리를 더 자주 사용하는게 현실입니다.

또 Promise 메소드를 자세히 살펴보시면 콜백 함수랑 뭔가 비슷한 점이 있지 않나요?

```jsx
loadScript("/article/promise-chaining/one.js").then(script1 => {
  loadScript("/article/promise-chaining/two.js").then(script2 => {
    loadScript("/article/promise-chaining/three.js").then(script3 => {
      // 여기서 script1, script2, script3에 정의된 함수를 사용할 수 있습니다.
      one();
      two();
      three();
    });
  });
});
```

맞습니다. Promise의 `.then()` 메소드도 인자로 콜백 함수를 받기 때문에, 까딱하다간 콜백 지옥에 또 빠져버리게 될 수 있어요.

하지만 아래와 같이 코드를 조금이나마 가독성 있게 고칠 수는 있습니다.

```jsx
loadScript("/article/promise-chaining/one.js")
  .then(script => loadScript("/article/promise-chaining/two.js"))
  .then(script => loadScript("/article/promise-chaining/three.js"))
  .then(script => {
    // 스크립트를 정상적으로 불러왔기 때문에 스크립트 내의 함수를 호출할 수 있습니다.
    one();
    two();
    three();
  });
```

이러한 방식을 `Promise chaining` 이라고 부릅니다. 위 코드와 비교했을 때 훨씬 가독성이 좋아지는 것을 확인할 수 있죠.

그렇지만 이런 단계가 많아지고 세분화될수록 `then`의 깊이가 점점 깊어지면서 가독성을 해치게 됩니다. 또한 Promise 기본 메소드만을 사용할 경우 하나의 함수 안에서 순서대로 동작하는 코드에 비동기 통신을 위한 코드 하나를 삽입하기 위해 번거롭게 데이터 통신용 함수를 하나 더 만들어야 하므로 귀찮음이 이만저만이 아니죠.

```jsx
function logName() {
  const user = fetchUser('domain.com/users/1');
	// fetchUser 함수는 인수로 넘겨받은 주소에 접근하면 user 정보 객체를 반환해준다고 가정해봅시다.
  if (user.id === 1) {
    console.log(user.name);
  }
}
```

위 코드가 순서대로 동작할까요? 아니라고 말하실겁니다. `fetchUser()의 동작이 끝난 후에 if 조건문이 실행되어야 해!` 라고 보장해주는 장치가 없기 때문이죠.

```jsx
function logName() {
  const user = fetchUser('domain.com/users/1', function(user) {
    if (user.id === 1) {
      console.log(user.name);
    }
  });
}
```

따라서 `fetchUser` 함수에 콜백함수가 들어갈 자리를 만들어주고 비동기 처리가 되어야 할 코드가 들어간 함수를 인자로 넘겨줘 처리시켜줘야 합니다. 만약 이 코드에서 그 다음 비동기 처리 코드가 있다면 또 콜백 자리를 파주어야겠죠.

하지만 `async / await` 를 알게 되면 나의 비동기 처리 성공 시대가 시작됩니다.

## Syntatic sugar for Promise  : async와 await

```jsx
// async & await 적용 후
**async** function logName() {
  const user = **await** fetchUser('domain.com/users/1');
  if (user.id === 1) {
    console.log(user.name);
  }
}ㅓ
```

`async / await` 를 배우지도 않았는데 단번에 이해가 되지 않으시나요? 심지어 기존 코드를 훼손시키지도 않고 그저 접두사 2개만 붙여주었을 뿐인데 위에서부터 아래로 순서가 보장이 되네요!

`async / await` 문법은 딱 세 가지만 알면 됩니다.

1. `await`는 반드시 `async` 가 붙은 함수 안에서만 동작한다.(일반 함수에서는 동작 안함)
2. 비동기 처리가 필요한 함수 앞에 `async` 접두사를 붙여주면 된다. 그럼 그 함수는 무족권 Promise 를 반환함!
3. 에러 핸들링은 `try { } catch { }`문법을 사용하면 된다.

```jsx
function f() {
  let promise = Promise.resolve(1);
  let result = await promise; // Syntax error
}
```

해당 코드는 에러를 뱉어낼거에요. Promise가 반환된 이후 `result`란 변수에 할당해주고 싶을 때엔 `.then()` 메소드 체이닝을 하거나 function 앞에 `async`를 붙여주면 됩니다.

위 코드를 구체화시키면 아래와 같습니다.

```jsx
async function f() {
  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("완료!"), 1000)
  });

  let result = await promise; // 프라미스가 이행될 때까지 기다림 (*)

  alert(result); // "완료!"
}

f();
```

`await` 접두사를 붙여줌으로써 코드 간의 순서를 보장해주었습니다. 또한 `async`가 붙은 함수는 무조건 Promise 객체를 반환하기 때문에(return문으로 특정 값을 반환토록 지정하면 Promise를 반환하지 않습니다 😅) 이후에 `.then()` 과 같은 메소드를 붙여 추가 처리를 해줄 수도 있어요. 

그래서 `async/await`를 사용하면 `promise.then/catch`가 거의 필요 없습니다. 하지만 가끔 가장 바깥 스코프에서 비동기 처리가 필요할 때 같이 `promise.then/catch`를 써야만 하는 경우가 생기기 때문에 `async/await`가 프라미스를 기반으로 한다는 사실을 알고 계셔야 합니다!

에러 핸들링 예시는 아래와 같습니다.

```jsx
async function f() {
  try {
    let response = await fetch('http://유효하지-않은-주소');
    let user = await response.json();
  } catch(err) {
    // fetch와 response.json에서 발행한 에러 모두를 여기서 잡습니다.
    alert(err);
  }
}

f();
```

Promise를 사용할 때와 달리, 함수 안에서 `await` 접두사를 통해 동기적 순서가 보장된 코드가 try문 안에 존재하므로 try문이 먼저 실행되고, 만약 Promise 객체의 상태가 rejected일 경우 catch 문으로 넘어가 에러가 처리되는 구조이죠.

.then().catch()보다 훨씬 더 직관적이지 않나요?

## 마무리

![Untitled](Week%204-3%20%E1%84%87%E1%85%B5%E1%84%83%E1%85%A9%E1%86%BC%E1%84%80%E1%85%B5%20%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%E1%84%8B%E1%85%AA%20Promise%20171bfaf23d4142b1a3a9a3fed11e8fd1/Untitled%207.png)

우리가 이번 시간 배운 Promise와 비동기 처리 방법들을 한 눈에 정리해주는 짤이 있어 가져와봤습니다. 이해가 확 되지 않으시나요?

Promise는 자바스크립트를 사용하는 프론트엔드 개발자에게 굉장히 중요한 개념입니다. 자바스크립트 기본 문법인 `fetch()`도 Promise를 반환하구요, 가장 많이 쓰이는 `axios` 라이브러리도 Promise 기반 라이브러리입니다. 간단한 코딩 연습으로는 콜백을 통해 비동기 프로세스를 이해할 순 있지만, 사이즈가 큰 데이터 통신을 다루기 위해선 Promise란 정해진 규칙이 필요합니다.

오늘 배운 내용은 중요한 내용이기 때문에 꼭 숙지하시기 바랍니다! 고생하셨습니다.

---

### 참고 자료 및 문헌

- [Promise - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [프라미스와 async, await - JAVASCRIPT.INFO](https://ko.javascript.info/promise-basics)
- [자바스크립트 비동기 처리와 콜백 함수 - 캡틴판교](https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/)
- [자바스크립트 Promise 쉽게 이해하기 - 캡틴판교](https://joshua1988.github.io/web-development/javascript/promise-for-beginners/)
- [Promise & async 못다한 이야기 - gil0127](https://velog.io/@gil0127/Promise-async-await)
- [비동기 프로그래밍 - JavaScript로 만나는 세상](https://helloworldjavascript.net/pages/285-async.html)