## React란?
- UI를 구성하는 JavaScript라이브러리
- 웹 앱(Web App)또는 네이티브 앱(Native App)
- 유지보수를 쉽게, DOM 관리
- 성능최적화를 쉽게
- 컴포넌트에 집중

## 컴포넌트
- UI를 구성하는 조각(piece)
- 독립적으로 분리되어 재사용 됨을 목적
- React 앱에서 컴포넌트는 개별적인 JavaScript파일로 분리되어 관리

### 함수형 컴포넌트
- 컴포넌트 외부로 속성(props)을 전달 받아 어떻게 UI를 구성해야 할지 설정하여 React 요소(JSX를 Babel이 변환 처리)로 반환하는 문법 구문을 사용하는 컴포넌트
```js
function Welcome(props){
    return (<h1>안녕, {props.name}</h1>);
}

export default Welcome;
```

### 클래스형 컴포넌트
- 자바스크립트의 ES6의 class라는 것을 사용해서 만들어진 형태의 컴포넌트이다.
- 컴포넌트의 구성 요소, 리액트 생명주기를 모두 포함하고 있다.
- 클래스형 컴포넌트의 경우 함수형 컴포넌트에 비해 몇가지 추가적인 기능을 가지고 있다.
```js
class Welcome extends React.Component{
	render(){
    	return <h1>안녕, {this.props.name}</h1>;
    }
}
```

## JSX
- JSX(JavaScript Syntax eXtension)
- React 엘리먼트(element)를 생성하는 JavaScript 확장 문법(React 요소는 실제 DOM요소가 아니라 JavaScript 객체이므로)

### JSX문법
1. 반드시 부모 요소 하나가 감싸는 형태여야 한다.
```js
// div를 사용 하였기 때문에 스타일 적용시 작성한 코드를 div로 한번 더 감쌌다는 부분을 고려해야 한다.
function App() {
	return (
		<div>
			<div>Hello</div>
			<div>GodDaeHee!</div>
		</div>
	);
}


function App() {
	return (
		<>
			<div>Hello</div>
			<div>GodDaeHee!</div>
		</>
	);
}
```

2. 자바스크립트 표현식
- JSX 안에서도 자바스크립트 표현식을 사용할 수 있다.
- 자바스크립트 표현식을 JSX내부에서 사용하려면 {}를 사용하면 된다.
```js
function App() {
	const name = 'GodDaeHee';
	return (
		<div>
			<div>Hello</div>
			<div>{name}!</div>
		</div>
	);
}
```

3. if,for문 대신 삼항 연산자 사용
- if문과 for문은 JavaScript 표현식이 아니기 때문에 JSX 내부 자바스크립트 표현식에서는 사용할 수 없다.
- 외부에서 사용하거나, {}안에서 삼항 연산자를 사용한다.
```js
//방법1 외부에서 사용
function App() {
	let desc = '';
	const loginYn = 'Y';
	if(loginYn === 'Y') {
		desc = <div>GodDaeHee 입니다.</div>;
	} else {
		desc = <div>비회원 입니다.</div>;
	}
	return (
		<>
			{desc}
		</>
	);
}

//방법2 내부에서 사용
function App() {
	const loginYn = 'Y';
	return (
		<>
			<div>
				{loginYn === 'Y' ? (
					<div>GodDaeHee 입니다.</div>
				) : (
					<div>비회원 입니다.</div>
				)}
			</div>
		</>
	);
}

//방법3 AND연산자(&&)사용
// 조건이 만족하지 않을 경우 아무것도 노출되지 않는다.
function App() {
	const loginYn = 'Y';
	return (
		<>
			<div>
				{loginYn === 'Y' && <div>GodDaeHee 입니다.</div>}
			</div>
		</>
	);
}
```

4. ReactDOM은 HTML 어트리뷰트 이름 대신 camelCase 프로퍼티 명명 규칙을 사용한다.
```js
//JSX에서 자바스크립트 문법을 쓰려면 {}를 써야 하기 때문에, 스타일을 적용할 때에도 객체 형태로 넣어줘야 한다.
//카멜 표기법으로 작성해야 한다. (font-size -> fontSize)
function App() {
	const style = {
		backgroundColor: 'green',
		fontSize: '12px'
	}
	return (
		<div style={style}>Hello, GodDaeHee!</div>
	);
}

//class 대신 className
//일반 HTML에서 CSS클래스를 사용할 때에는 class라는 속성을 사용한다.
//JSX에서는 class가 아닌 className을 사용한다.
function App() {
	const style = {
		backgroundColor: 'green',
		fontSize: '12px'
	}
	return (
		<div className="testClass">Hello, GodDaeHee!</div>
	);
}
```
5. JSX 내에서 주석 사용 방법
- {/* ... */}와 같은 형식을 사용한다.
```js
function App() {
	return (
		<>
			{/* 주석사용방법 */}
			<div>Hello, GodDaeHee!</div>
		</>
	);
}
```

### 주의사항
- 태그는 반드시 닫는다.
- 최상단에서는 반드시 div 혹 Fragment<>로 감싸줘야 함
- JSX 안에서 자바스크립트 값을 사용하고 싶을 때는 {}를 사용
- 조건부 렌더링을 하고 싶으면 &&연산자나 삼항연산자를 사용
- 인라인 스타일링은 항상 객체 형식으로 작성
- 별도의 스타일 파일을 만들었으면 class 대신 className 사용
- 주석은 {/* */}을 사용

## Vite로 만든 React 프로젝트의 구조
- 만들어진 Vite 프로젝트를 보면 index.html이 public 디렉토리가 아닌 프로젝트의 루트(root)에 위치해 있는 것을 볼 수 있다.
- 추가적인 번들링 과정 없어 index.html 파일이 앱의 진입점이 되게끔 하기 위함이다.

![image](img/index.png)

### 구성
- index.html: 웹 브라우저에 로드되는 정적 HTML파일이다. React 애플리케이션을 초기화하고 렌더링하는 중요한 역할을 수행한다.
- package.json: 프로젝트의 의존성과 스크립트를 정의한 파일입니다.
- public: 정적 파일을 저장하는 디렉토리입니다.
- src: React 애플리케이션의 소스코드를 저장하는 디렉토리입니다.
- src/main.jsx: React 애플리케이션의 논리적인 진입점입니다.
- vite.config.js: Vite 설정 파일입니다.

## React 작동 순서
### 1. 초기화
- main.jsx 파일에서 React앱을 초기화 한다.
- 이 과정에서 ReactDOM의 'render'함수를 사용하여 React앱의 루트 컴포넌트를 실제 DOM에 렌더링 한다.

<p align="center">
  <img src="img/init_render.png">
</p>

### 2. 가상 DOM 생성
- React는 컴포넌트의 상태(State)나 속성(Properties)의 변화에 따라 가상 DOM을 생성한다.
- 가상 DOM은 실제 DOM을 추상화한 것으로, 메모리에 존재하며 브라우저에 실제로 렌더링 되지 않는다.