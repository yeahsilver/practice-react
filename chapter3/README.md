# 3. JSX

## 컴포넌트 파헤치기

컴포넌트에 해당하는 코드는 App.js에서 확인할 수 있음

```react
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h1 className="App-title">Welcome to React</h1>
        </header>
        <p className="App-intro">
          To get started, edit <code>src/App.js</code> and save to reload.
        </p>
      </div>
    );
  }
}

export default App;
```



import한다는 것은 무엇을 불러온다는 뜻임.

import를 하는 것은 우리가 webpack을 사용하기에 가능한 작업임. 이렇게 불러오고 나면 나중에 프로젝트를 빌드하게 되었읐 때 웹팩에서 파일의 확장자에 따라 다른 작업을 하게 됩니다. CSS파일을 불러오게 되면, 나중에 프로젝트에서 사용한 프로젝트를 한 파일에 모두 결합해주는 작업을 진행하고, 자바스크립트 파일을 불러오게 되면 모든 코드들이 제대로 로딩되게끔 순서를 설정하고 하나의 파일로 합쳐줌.

```react
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';
```



#### 컴포넌트를 만드는 방법

클래스를 통해서 만드는 방법

```react
class App extends Component {
  ...
}
```

클래스 형태로 만들어진 컴포넌트에는 꼭 render 함수가 존재해야함. 그리고 그 내부에서는 JSX를 반환하여야 한다. 

```react
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h1 className="App-title">Welcome to React</h1>
        </header>
        <p className="App-intro">
          To get started, edit <code>src/App.js</code> and save to reload.
        </p>
      </div>
    );
  }
```



작성한 컴포넌트를 다른 곳에 불러와서 사용할 수 있도록 내보내기해줌

```react
export default App;
```



브라우저 상에서 리액트 컴포넌트를 보여주기 위해서는 ReactDOM.render 함수를 사용한다. 첫번째 파라미터는 렌터링 할 결과물이고, 두번째 파라미터는 컴포넌트를 어떤 DOM에 그릴지 정해줌

```react
ReactDOM.render(<App />, document.getElementById('root'));
registerServiceWorker();
```



id가 root인 DOM을 찾아서 그리도록 설정되어있는데, 해당 파일안에 있는

```react
<div id="root"></div>
```

를 찾아 렌더링 해주는 것이다 .

