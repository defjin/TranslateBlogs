Learn React JS in 5 minutes — A tutorial for beginners
https://medium.com/free-code-camp/learn-react-js-in-5-minutes-526472d292f4

ReactJS 5분만에 배우기. 초보자를 위한 튜토리얼

몇 분만에 유명한 자바스크립트 라이브러리를 시작해봅시다.

2018.4.11

이 튜토리얼은 매우 단순한 어플리케이션을 만들어보면서 여러 분에게 리액트의 기초에 대해서 알려줄 것입니다. 
내 생각에 중요하지 않은 부분은 남겨두겠습니다. 

그리고 여러 분이 흥미가 생겨서 더 배우고 싶어진다면, 우리의 무료 리액트 수업(https://scrimba.com/g/glearnreact) 수업을 확인해보세요.

지금은 기초에 집중해봅시다!

## The Setup
리액트를 시작할 때, 여러분은 가능한 단순한 설정을 사용해야합니다. 
script tag를 이용해서 React 와 ReactDOM 을 임포트한 HTML 파일을 보죠. 

다음과 같이 생겼습니다. 
``` HTML
<html>
<head>
<script src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
<script src="https://unpkg.com/babel-standalone@6.15.0/babel.min.js"></script>
</head>
<body>
    <div id="root"></div>
    <script type="text/babel">
    
    /* 
    ADD REACT CODE HERE 
    */
    
    </script>
</body>
</html>
```

 우리는 Babel도 임포트했습니다. 리액트는 JSX라고 불리는 마크업을 작성하는데 사용하기 때문이죠.
 우리는 브라우저가 그 내용을 이해할 수 있도록 JSX를 일반적인 Javascript로 바꿔야합니다. 

 여러분이 알아야할 것이 2개가 더 있습니다. 
 1. id가 #root인 `<div>`가 있습니다. 이것이 우리 어플리케이션의 진입점입니다. 여기에서 우리 어플리케이션 전체가 살아있을 곳입니다.
 2. body에 `<script type="text/babel">` 태그가 있습니다. 우리의 리액트 코드를 여기에 작성할 것입니다.

만약 코드를 실험해보길 원한다면, Scrimba playground (https://scrimba.com/c/cmGe8Cp) 를 확인해보세요


## Components
리액트의 모든 것은 '컴포넌트'입니다. 그리고 이것들은 일반적으로 자바스크립트 클래스의 형태를 가지고 있습니다. 
여러분은 React-Component 라는 클래스를 확장해서 새로운 컴포넌트를 만들 수 있습니다. 
Hello라는 컴포넌트를 만들어봅시다. 

``` jsx
class Hello extends React.Component {
    render() {
        return <h1>Hello world!</h1>;
    }
}
```

이제 컴포넌트의 메소드를 정의할 수 있습니다. 우리의 예제에서는 하나의 메소드만 가지고 있고, 이건 redner()라고 불립니다.
render() 안에서 여러분이 페이지 위에서 React가 그리길 원하는 것에 대한 묘사를  돌려주게 됩니다. 
위의 케이스에서는, 단순하게 Hello World! 라는 텍스트를 가지고 있는 h1 태그를 보여주길 원했습니다. 

우리의 조그만 어플리케이션을 스크린 위에 렌더하기 위해서 우리는 ReactDOM.render()를 사용해야합니다. 

``` javascript
ReactDOM.render(
    <Hello />,
    document.getElementByID("root")
)
```

바로 여기에서 우리의 Hello 컴포넌트를 앱의 시작점(<div id="root"></div>)과 연결합니다. 

단순하게 말하자면 다음과 같습니다. : 이봐 리액트! Hello 컴포넌트를 root라는 id를 가진 DOM 노드 안에 렌더해줘.

결과는 다음과 같습니다. 

``` HTML
<h1>Hello world!<h1>
```

`<h1>`과 `<Hello/>`에서 같은 HTML 같은 문법이 앞에서 언급했던 JSX 코드입니다. 이것은 HTML은 아니고, 더 파워풀합니다. 
작성하는 내용이 DOM에 HTML 태그로 표시됩니다.

다음 스텝은 우리의 어플리케이션이 데이터를 다룰 수 있게 하는 것입니다.


## Handling data

리액트에는 두 종류의 데이터가 있습니다. props 와 state 입니다. 둘 사이의 차이는 시작 단계에서 이해하기에는 조금 까다롭습니다. 그래서 약간 헷갈리는 부분을 찾는다고 걱정하진 마세요. 그것들을 일단 만져보기 시작하면 점점 쉬워질 것입니다.

가장 핵심적인 차이는  state는 private 이고, 자기 컴포넌트 안에서만 바뀔 수 있다는 것입니다. Props는 외부에서 오는 것이고 내부에서 다룰 수는 없습니다. 데이터를 다루는 상위 컴포넌트에서 넘겨받습니다. 

컴포넌트는 내부 state를 직접 변경할 수 있습니다. props는 직접 변경할 수 없습니다. 

먼저 props를 자세히 살펴봅시다. 

## Props
Hello 컴포넌트는 완전히 정적입니다. 어떤 경우에도 항상 같은 메세지를 렌더합니다. 그러나 리액트의 매우 중요한 부분은 재사용성입니다. (컴포넌트를 한 번 작성하고, 다른 케이스에서 다시 사용할 수 있는 것을 뜻합니다.) 

다른 메시지를 보여주는 예를 봅시다. 

이런 유형의 재사용성을 얻기 위해서는, 우리는 props를 추가할 것입니다. props를 컴포넌트에 전달하는 방법은 다음과 같습니다. 

``` javascript
ReactDOM.render(
    <Hello message="my friend" />, document.getElementByID("root")
)
```

이 prop은 message 로 불리며, "my friend"라는 값을 가집니다. 헬로우 컴포넌트 안에서는 this.props.message 를 참조해서 접근할 수 있습니다. 

``` jsx
class Hello extends React.Component {
    render() {
        return <h1>Hello {this.props.message}! </h1>;
    }
}
```
다음의 결과가 화면에 렌더됩니다.
``` HTML
<h1> Hello my friend!</h1>
```

{ this.props.message }로 작성한 이유는 JSX에게 자바스크립트 표현식을 추가하기를 원한다는 것을 말해야하기 때문입니다. 이것을 escaping 이라고 합니다. 

이제, 페이지에 렌더하길 원하는 어떤 메시지도 쓸 수 있는 재사용가능한 컴포넌트를 가지게 되었습니다. 

## State 
리액트에서 데이터를 저장하는 다른 방법은 컴포넌트의 state를 이용하는 것입니다. props와는 다르게 state는 컴포넌트에서 직접적으로 값을 변경할 수 있습니다. 

만약, 여러분의 어플리케이션에서 데이터가 바뀌길 원한다면, 어플리케이션 어딘가의 컴포넌트의 state에 반드시 저장되어야합니다. (예를 들어서 사용자 상호작용에 기반한다면...)

## Initializing state
state를 초기화하기 위해서 this.state를 클래스의 constructor() 메소드에서 정할 수 있습니다. 우리의 state는 message라는 키 값을 가지는 object입니다. 

``` jsx
class Hello extends React.Component {
    constructur() {
        super();
        this.state = {
            message: "my friend (from state) !"
        };
    }

    render(){
        return <h1>Hello {this.state.message}!</h1>;
    }
}
```

 우리가 state를 정하기 전에 생성자에서 super()를 호출해야합니다. super()가 호출되기 전에는 this가 초기화되지 않기 떄문입니다. 

 ## Chainging the state
 state를 변경하기 위해서, 간단히 새로운 state object를 인수로 전달하여 this.setState() 를 호출하면 됩니다. 이것을 updateMessage라는 메소드 안에서 작동시켜보겠습니다. 

 ``` jsx 
 class Hello extends React.Component {
     constructor() {
         super();
         this.state = {
             message: "my friend (from state)!"
         };
         this.updateMessage = this.updateMessage.bind(this);
     }

     updateMessage() {
         // 1번 this
         this.setState({
             message: "my friend (from changed state)!"
         });
     }

     render() {
         return <h1>Hello { this.state.message}!</h1>;
     }
 }
 ```

 위의 코드가 동작하려면 반드시 this 키워드를 updateMessage 메소드에 바인드해줘야합니다. 그렇지 않으면 메소드 안에서 1번 this에 접근할 수 없습니다. 

 ## Event Handlers 
다음 단계로 클릭할 수 있는 버튼을 만들어봅시다. 그것으로 updateMessage를 작동시킬 수 있습니다.
render() 메소드에 버튼을 추가해보죠

``` jsx
render() {
    return (
        <div>
            <h1>Hello {this.state.message}!</h1>
            <button onClick={this.updateMessage}>Click me!</button>
        </div>
    )
}
```

여기서 onClick 이벤트를 듣고 있는 이벤트 리스너를 버튼에 연결했습니다. 이게 작동되면, updateMessage라는 메소드를 호출합니다. 

전체 컴포넌트는 다음과 같습니다.

``` jsx
class Hello extends React.Component {
    
    constructor(){
        super();
        this.state = {
            message: "my friend (from state)!"
        };
        this.updateMessage = this.updateMessage.bind(this);
    }
    updateMessage() {
        this.setState({
            message: "my friend (from changed state)!"
        });
    }
    render() {
         return (
           <div>
             <h1>Hello {this.state.message}!</h1>
             <button onClick={this.updateMessage}>Click me!</button>
           </div>   
        )
    }
}
```

updateMessage 메소드는 this.setState()를 호출합니다. 이것은 this.state.message 값을 변경합니다. 그리고 우리가 버튼을 누르면 다음과 같이 동작합니다.

축하합니다.! 이제 여러분은 리액트의 가장 중요한 개념의 기초를 이해했습니다. 더 많은 것을 배우길 원한다면 https://scrimba.com/g/glearnreact 를 확인해보세요. 

