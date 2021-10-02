# 김시온 [201840111]
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