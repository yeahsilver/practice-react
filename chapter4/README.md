# 4. props와 state
- props: 부모 컴포넌트가 자식 컴포넌트에게 주는 값. 컴포넌트에서는 props를 받아오기만 하고, 받아온 props를 직접 수정할 수 없음.
- state: 컴포넌트 내부에서 선언하며 내부에서 값을 변경할 수 있음.

</br>

## 새 컴포넌트 만들기
> .src 디렉토리에 MyName 컴포넌트 생성

``` react
import React, { Component } from 'react';

class MyName extends Component {
  render() {
    return (
      <div>
        안녕하세요! 제 이름은 <b>{this.props.name}</b> 입니다.
      </div>
    );
  }
}

export default MyName;

```

자신이 받아온 props값은 this. 키워드를 통하여 조회할 수 있음.
지금 name이라는 props를 보여주도록 설정함.

App.js
``` react
import React, { Component } from 'react';
import MyName from './MyName';

class App extends Component {
  render() {
    return (
      <MyName name="리액트" />
    );
  }
}

export default App;

```

import를 통하여 컴포넌트를 불러오고, 렌더링. 

</br>

## defaultProps
가끔씩은 실수로 props를 빠뜨려먹을 떄가 있다. 혹은 특정 상황에서 일부러 props를 비워야하는 경우도 있다. 이러한 경우에 props의 기본값을 설정할 수 있는데, 그것이 바로 defaultProps이다.


```
import React, { Component } from 'react';

class MyName extends Component {
  static defaultProps = {
    name: '기본이름'
  }
  render() {
    return (
      <div>
        안녕하세요! 제 이름은 <b>{this.props.name}</b> 입니다.
      </div>
    );
  }
}

export default MyName

```

이런식으로 사용하게 된다면, 만약 <MyName />에서 name값을 생략해버리면 "기본 이름"이 나타나게 됨.

defaultProps는 다음과 같은 형태로도 설정할 수 있다.


```
import React, { Component } from 'react';

class MyName extends Component {
  render() {
    return (
      <div>
        안녕하세요! 제 이름은 <b>{this.props.name}</b> 입니다.
      </div>
    );
  }
}

MyName.defaultProps = {
  name: '기본이름'
};

export default MyName;

```

</br>

함수형 컴포넌트
단순히 props만 받아와서 보여주기만 하는 컴포넌트의 경우엔 더 간편한 문법으로 작성할 수 있는 방법이 존재한다. 그것이 바로 함수이다. 


```
import React from 'react';

const MyName = ({ name }) => {
  return (
    <div>
      안녕하세요! 제 이름은 {name} 입니다.
    </div>
  );
};

export default MyName;
```

함수형 컴포넌트와 클래스형 컴포넌트의 주요 차이점은, state와 lifecycle이 빠져있다는 점이다. 그래서 컴포넌트 초기 마운트가 아주 미세하게 빠르고 메모리 자원을 덜 사용한다. 

</br>

## State
동적인 데이터를 다룰 때 사용.

```
import React, { Component } from 'react';

class Counter extends Component {
  state = {
    number: 0
  }

  handleIncrease = () => {
    this.setState({
      number: this.state.number + 1
    });
  }

  handleDecrease = () => {
    this.setState({
      number: this.state.number - 1
    });
  }

  render() {
    return (
      <div>
        <h1>카운터</h1>
        <div>값: {this.state.number}</div>
        <button onClick={this.handleIncrease}>+</button>
        <button onClick={this.handleDecrease}>-</button>
      </div>
    );
  }
}

export default Counter;
```

### State 정의
컴포넌트의 state를 정의할 떄는 class fields 문법을 사용하여 정의

```
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      number: 0
    }
  }

  ...

 
}

```

위 코드의 constructor에서 super(props)를 호출한 이유는,우리가 컴포넌트를 만들게 되면서, Component를 상속했으며, 우리가 이렇게 constructuor를 작성하게 되면 기존의 클래스 생성자를 덮어쓰게 됩니다. 그렇기에, 리액트 컴포넌트가 지니고 있던 생성자를 super를 통해 미리 실행하고, 그 다음에 우리가 할 작업 (state 설정)을 해줌.

