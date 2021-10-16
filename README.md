# 김시온 [201840111]

---
## [10월 13일]
##### 오늘 배운 내용 요약

# axios 기본에 대해서

### REST API
```
REST API는 우리가 하고싶은 작업에 따라 다른 메서드로 요청할 수 있는 것

REST API에는 대표적으로 다음과 같은 HTTP 메서드를 행위의 수단으로 이용
    GET : 데이터 조회
    POST : 데이터 등록 및 전송
    PUT : 데이터 수정
    DELETE : 데이터 삭제
```

### axios 설치하기
```
npm 사용하기
$ npm install axios

yarn 사용하기
yarn add axios

bower 사용하기
$ bower install axios

jsDeliver CDN 사용하기
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>

unpkg CDN 사용하기
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

### axios 사용하기
```
axios에서 Request Method를 사용하기 위해서는 axios에 .을 붙히며 소문자로 Req Method를 넣어주면 된다.
그리고 해당 메서드의 파라미터에는 API의 주소를 넣는다.
GET : axios.get(url[, config])
POST : axios.post(url, data[, config])
PUT : axios.put(url, data[, config])
DELETE : axios.delete(url[, config])
```

### 일반적인 axios
```
일반적으로 우리는 axios의 4가지 기본 메서드를 사용하기 위해 지정해야할 것들이 있다.
4가지 기본 Params
    Method
    Url
    Data (optional)
    Params (optional)
이 4가지 방법을 axios에 알려줘야 한다.

axios({
    method: "get",
    url: "url",
    responseType: "type"
}).then(function (response) {
    // response Action
});
위와 같이 사용하는 것이 가장 기본적인 axios에 대한 사용법이다.
만약 POST 메서드에서 data를 전송하기 위해서는 url 밑에 data Object를 추가하면 된다.
```

### 단축된 axios 메서드
```
단축된 axios의 메서드를 사용해서 위의 4가지 기본 파라미터를 생략하거나 간결하게 사용할 수 있다.

1. axios.get()
get 메서드를 단축된 속성으로 사용하려면 get 메서드를 사용하면 된다.
get 메서드에는 2가지 상황이 크게 존재한다.
단순 데이터(페이지 요청, 지정된 요청) 요청을 수행할 경우
파라미터 데이터를 포함시키는 경우 (사용자 번호에 따른 조회)
2가지 상황에 따라 params: {} 객체가 존재할지 안할지가 결정된다.

2. axios.post()
post 메서드에는 일반적으로 데이터를 Message Body에 포함시켜 보낸다.
위에서 봤던 get 메서드에서 params를 사용한 경우와 비슷하게 수행된다.

3. axios.put()
put 메서드는 서버 내부적으로 get -> post 과정을 거치기 때문에 post 메서드와 비슷한 형태이다.

4. axios.delete()
delete 메서드에는 일반적으로 body가 비어있다.
그래서 형태는 get과 비슷한 형태를 띄지만 한 번 delete 메서드가 서버에 들어가게 된다면 서버 내에서 삭제 process를 진행하게 된다.
```


---
## [10월 6일]
##### 오늘 배운 내용 요약

### constructor()
```
constructor() 내부에서 setState()를 호출하면 안됨. 컴포넌트에 지역 state가 필요하다면 생성자 내에서 this.state에 초기 state 값을 할당
ex)
constructor(props) {
  super(props);
  // 여기서 this.setState()를 호출하면 안 됩니다!
  this.state = { counter: 0 };
  this.handleClick = this.handleClick.bind(this);
}
```

### componentDidMount()
```
componentDidMount()는 컴포넌트가 마운트된 직후, 즉 트리에 삽입된 직후에 호출
DOM 노드가 있어야 하는 초기화 작업은 이 메서드에서 이루어지면 됨
외부에서 데이터를 불러와야 한다면, 네트워크 요청을 보내기 적절함

이 메서드는 데이터 구독을 설정하기 좋음. 
데이터 구독이 이루어졌다면, componentWillUnmount()에서 구독 해제 작업을 반드시 수행해야 함

componentDidMount()에서 즉시 setState()를 호출하는 경우도 있는데,
이로 인하여 추가적인 렌더링이 발생하지만, 브라우저가 화면을 갱신하기 전에 이루어짐
이런 사용 방식은 성능 문제로 이어지기 쉬우므로 주의가 필요
대부분의 경우, 앞의 방식을 대신하여 constructor() 메서드에서 초기 state를 할당할 수 있음
하지만 모달(Modal) 또는 툴팁과 같이 렌더링에 앞서 DOM 노드의 크기나 위치를 먼저 측정해야 하는 경우 이러한 방식이 필요
```

### componentDidUpdate()
```
componentDidUpdate()는 갱신이 일어난 직후에 호출됨, 최초 렌더링에서는 호출되지 않음

컴포넌트가 갱신되었을 때 DOM을 조작하기 위하여 이 메서드를 활용하면 좋음
이전과 현재의 props를 비교하여 네트워크 요청을 보내는 작업도 이 메서드를 사용

componentDidUpdate()에서 setState()를 즉시 호출할 수도 있지만, 위의 예시처럼 조건문으로 감싸지 않으면 무한 반복이 발생할 수 있다는 점에 주의
추가적인 렌더링을 유발하여, 비록 사용자는 눈치채지 못할지라도 컴포넌트 성능에 영향을 미칠 수 있음
상위에서 내려온 prop을 그대로 state에 저장하는 것은 좋지 않으며, 그 대신 prop을 직접 사용하는 것이 좋음

컴포넌트에서 getSnapshotBeforeUpdate()를 구현한다면, 해당 메서드가 반환하는 값은 componentDidUpdate()에 세 번째 “snapshot” 인자로 넘겨지고, 반환값이 없다면 해당 인자는 undefined를 가짐
```

### componentWillUnmount()
```
componentWillUnmount()는 컴포넌트가 마운트 해제되어 제거되기 직전에 호출
이 메서드 내에서 타이머 제거, 네트워크 요청 취소, componentDidMount() 내에서 생성된 구독 해제 등 필요한 모든 정리 작업을 수행

이제 컴포넌트는 다시 렌더링되지 않으므로, componentWillUnmount() 내에서 setState()를 호출하면 안됨
컴포넌트 인스턴스가 마운트 해제되고 나면, 절대로 다시 마운트되지 않음
```


---
## [9월 29일]
##### 오늘 배운 내용 요약

### prop-types
```
작업하는 프로젝트의 규모가 커질 수록 생각지 못한 곳에서 에러가 발생하는 일이 잦아짐
이를 방지하기 위한 방법으로, PropTypes를 활용하여 타입(type)을 확인하는 것이 대표적
PropTypes는 부모로부터 전달받은 prop의 데이터 type을 검사
자식 컴포넌트에서 명시해 놓은 데이터 타입과 부모로부터 넘겨받은 데이터 타입이 일치하지 않으면 콘솔에 에러 경고문이 띄워짐
```

### prop-types 종류
```
MyComponent.propTypes = {
  // 리액트 요소
  // <div>123</div> , <Component />
  menu: PropTypes.element,
  
  // 컴포넌트 함수가 반환할 수 있는 모든 것(비추)
  // <SomeComponent />, 123
  description: PropTypes.node,
  
  // Message 클래스로 생성된 모든 객체
  // new Messages() -> 참, new Car() -> 거짓
  message: PropTypes.instanceOf(Message),
  
  // 배열에 포함된 값 중에서 하나를 만족
  name: PropTypes.oneOf(["jake", "olivia"]),

  // 배열에 포함된 타입 중에서 하나를 만족
  width: PropTypes.oneOfType([PropTypes.number, PropTypes.string])

  // 특정 타입만 포함하는 배열
  // [1, 5, 7] -> 참, ['a', 'b'] -> 거짓
  ages: PropTypes.arrayOf(PropTypes.number),

  // 객체의 속성값 타입을 정의
  // {color: 'red', weight: 123} -> 참
  info: PropTypes.shape({
    color: PropTypes.string,
    weight: PropTypes.number
  })

  // 객체에서 모든 속성값의 타입이 같은 경우
  // {prop1: 123, prop2: 456}
  infos: PropTypes.objectOf(PropTypes.number)
}
```

### state
```
props처럼 App 컴포넌트의 렌더링 결과물에 영향을 주는 데이터를 갖고 있는 객체
props는 (함수 매개변수처럼) 컴포넌트에 전달되는 반면 state는 (함수 내에 선언된 변수처럼) 컴포넌트 안에서 관리
props를 사용했는데도 state를 사용하는 이유는, 사용하는 쪽과 구현하는 쪽을 철저하게 분리시켜서 양쪽의 편의성을 각자 도모하는 것에 있다.
```

### State와 Props의 차이점
```
화면에 출력되는 내용은 완전히 똑같지만, props 데이터를 사용자에게 노출되는 부분에 직접 적는 것이 아니라 State를 통해 참조했다는 차이가 있다.
사용자가 알 필요가 없는 데이터를 내부에서 은닉하는 것
    즉, 캡슐화를 통해 코드를 리펙토링 하는 것이 좋은 사용성을 만드는 핵심
```


---
## [9월 15일]
##### 오늘 배운 내용 요약

### props
```
컴포넌트에서 컴포넌트로 전달되는 데이터
props를 사용하여 컴포넌트를 효율적으로 사용
props의 전달 데이터는 문자열인 경우를 제외하면 모두 {}로 감싸야 한다.
객체의 특정 값 사용 시 .(점) 사용
구조 분해 할당 사용 시 점 연산자를 사용하지 않아도 된다.
```

### map() 함수
```
배열의 모든 원소마다 특정 작업을 하는 함수를 적용하고, 그 함수가 반환한 결과를 모아서 배열로 반환해 준다.
```


---
## [9월 08일]
##### 오늘 배운 내용 요약

# 슈퍼 빠른 create-react-app


### create-react-app으로 앱 만들기
```
명령 프롬프트를 실행한 다음 리액트 앱을 만들고 싶은 곳으로 이동하고 명령으로 movie_app_2021라는 폴더를 만들어 본다.
npx create-react-app movie_app_2021 라고 사용한다.
```

### 로컬 저장소 초기화하기
```
git init 명령어를 실행하면 저장소를 초기화한다.
```

### 깃허브에 저장소 만들기
```
깃허브 저장소 만들게 페이지에 접속해서 깃허브랑 vscode를 연결하고 커밋을 하고 푸쉬를 한다.
푸쉬가 완료되면 깃허브 저장소를 확인해보면 변경된 README.md 파일의 내용도 보인다.
```

### 리액트 앱 실행하기
```
명령 프롬프트에서 루트 폴더로 이동한 다음  npm start를 입력한다.
명령 프롬프트에 'Compiled Successfully!'와 같은 문장이 보인 다음, 크롬 브라우저가 켜지고 다음 화면이 나타나면 OK야! 리액트 앱이 실행되었다.
리액트 종료하려면 Ctrl + c를 누르면 리액트 앱이 종료된다.
```

### 리액트 동작 원리 알아보기
```
리액트는 우리가 작성한 프로젝트 폴더에 있는 코드를 자바스크립트를 이용하여 해석하고 해석한 결과물을 index.html로 끼워 넣는다.
그래서 index.html 파일에 없던 <div>Hello!!!!<!div>가 리액트 앱을 실행하면 생긴다.
```

### index.js 파일로 컴포넌트의 사용 알아보기
```
<App />부분을 ReactDOM.render(<App />, document.getElementById('root'));로 바꾼다.
APP 컴포넌트가 변환하는 것들을 화면에 그릴 수 있고 App 컴포넌트가 그려질 위치는 ReactDOM.render() 함수의 두 번쨰 인자로 전달하면 된다.
리액트는 컴포넌트와 함께 동작하고, 리액트 앱은 모두 컴포넌트로 구성된다.
```