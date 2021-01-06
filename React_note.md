# Section. 1

```
npx create-react-app myapp
```

```
npm start
```



###### Module Systems

- ES2015 Modules : import
- CommonJS Modules : require



# Section. 2

브라우저는 jsx 이해못함. 그래서 javascropt 코드로 변환 필요함. 그게 **Babel**임. 

ex) React.createElement() 를 호출해서 jsx에 쓰여진 대로 컴포넌트 생성함.

jsx로 안쓰고 js로 쓰면 이해하기 복잡함. 구조 더러움. 그래서 jsx 쓰는거임.

Babel은 ES2015 이상의 javascript 코드를 ES5로 바꿔주는 역할도 함.



물론 html이랑 jsx는 다름.

##### < Html과 jsx가 다른점 >

- Jsx에 Inline style 넣을라면 { }안에 객체 { }로 넣어야 함. 속성명에 – 들어가면 없애고 camelCase로 바꿔줌.
- Jsx에 class 넣을라면 class대신 className 써야함. / 근데 요즘 기술 좋아져서 class 써도 알아들음. 그래서 나중엔 className말고 걍 class 쓰라고 문서에 나올수도?
- Jsx는 js 변수,함수를 참조할 수 있다. { } 안에 넣으면 됨-> 컴포넌트 동적생성이 가능하도록 하는 기능!! 특히 무언가를 출력할 때 변수는 string, number, array 등 다 되지만 object는 안됨!!! Inline style에 object 넣는거랑은 다름. 헷갈리면 안된다. object.property 이렇게는 된다. 

è 얘네 말고도 jsx랑 html 사이에 다른거 있는데, 세상 좋아져서 오류는 안난다. 근데 콘솔 열어보면 warning 메시지 보일거야. 그거 보고 수정해라.



# Section. 3

Component

- Nesting
- Reusability
- Configuration



```
npm install --save faker
```

--save 를 쓰면 local storage에 설치하고, dependency를 추가해준다.



###### Reusable component를 만들기 위해서

1. 중복해서 사용되는 구조를 파악한다
2. component에 **적절한 이름**을 붙인다
3. component랑 **같은 이름**을 가진 파일을 만든다
4. 그 안에 새로운 component를 만든다



###### Prop system

**parent** component 에서 **child** component로 **data**를 넘겨주는 것

child component로 object로 넘어감. 그래서 object 그대로 쓰면 안되고 prop 지정해서 써야함.

why? jsx에선 object 못쓰잖아!



근데 단순히 하드코딩된 값을 넘기는게 아니라 prop에 다른 component를 넘길수도 있음.

이 경우 props에 children으로 들어감!

```jsx
<ApprovalCard>
    <CommentDetail
      author="Sam"
      timeAgo="Today at 4:45PM"
      content="one"
      profile={faker.image.image()}
    />
</ApprovalCard>
```

만약에 component 여러개 넘기면 child가 object가 아니라 array 되고 그 안에 object로 담김.



# Section. 4

component는 **Function / Class**이고

- JSX를 사용해서 유저에게 보여줄 HTML를 생성하거나
- event handler를 사용해서 유저의 피드백을 처리한다

이번 섹션에선 **Class** 형태의 **component**에 대해 알아보자!

![image-20210105151506523](C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20210105151506523.png)

![image-20210105151520710](C:\Users\K\AppData\Roaming\Typora\typora-user-images\image-20210105151520710.png)



과거엔 function components는 html 생성밖에 못했음. 근데 **hooks** 가 추가?되면서 둘이 비슷해짐.

그래서 과거부터 react 써서 개발한데는 class components 위주로 사용했을 것이고(그땐 function의 사용처가 제한적이었으니까)

최근 react로 개발하기 시작한데는 class/function 둘다 쓸 수 있겠지.

근데 결국 둘다 알아야함ㅋ



여기선 class components / state system / lifecycle methods 배우고 Hooks, Redux 배울거얌.

바로 Hooks / Redux 들어가면 어려움.



function 구조로 짜서 사용자의 위치를 가져온다고 해보자.

1. 브라우저가 js파일 읽고
2. component 생성하고
3. getCurrentPosition()로 위치 가져오게 하고
4. 근데 위치 오기 전에 JSX return 시켜버림. 위치 가져오는데 오래걸려서!
5. return 이후에 위치 구함. 의미없지?



그럼 class 기반으로 하면 어떨까?

먼저

```js
class App extends React.Component
```

에서 extend 하는건 저기 설정되어 있는 method 가져다 쓸라고 하는거.

그리고 class 기반 component는 jsx 리턴하는 render() method 정의되어야함. 아니면 error

근데 function 구조 그대로 class로 바꾸면 해결되는거 없음.

핵심은 **state**를 쓰는거!!



state랑 prop 헷갈리지 마



###### State : component랑 관련된 data를 갖고 있는 JS object

- state를 update하면 해당 component만 re-render 된다?
- state는 component가 생성될때 initialized 되어야 한다
- *state는 **setState()**를 통해서만 update될 수 있다.*



# Section. 5

state 업데이트 할 때

```js
this.state.lat = position.coords.latitude;
```

이렇게 직접 대입해버리면 **절!대! 안된다.**

직접 대입하는건 constructor 안에서 initialize 할때밖에 없음!!!

```js
this.setState({ lat: position.coords.latitude });
```

이렇게 하는거임.



# Section. 6

data-load하는 두가지 방법

- constructor() 에서 
- component lifecycle method(componentDidMount()) 안에서 

기술적으론 어디에서 해도 괜찮은데. 공식문서나 커뮤니티 컨벤션은 componentDidMount()에서 대입하는거임.

코드 혼자짤거 아니잖아? 컨벤션 지키렴. **data-loading은 무조건 componentDidMount()**임!!



##### Component Lifecycle

1. constructor() : one-time setup 두기 좋은 장소. 
2. render() : **매우 자주 호출되므로, 가볍게 해야함. JSX만 리턴하도록 유지!!!**
3. componentDidMount() : **data-loading** 하기 좋음
4. setState()로 업데이트 발생하면 render() 다음에 componentDidUpdate() : **업데이트 될때마다 data-loading** 해야하는 코드 쓰기 좋음
5. component 지워지면 componentWillUnmount() : **cleanup** 하기 좋음.
6. 이거 말고도  sholdcomponentupdate, getderivedstatefromprops, getsnapshotbeforeupdate 같은 method도 있지만 아주 가~아끔 사용하므로 나중에 필요할때 찾아보렴!



state initialize할 때

```js
  constructor(props) {
    super(props);

    this.state = { lat: null, errorMessage: null };
  }
```

이렇게 constructor()안에 쓰는거 말고

```js
class App extends React.Component {
  state = { lat: null, errorMessage: null };
}
```

그냥 이렇게 app class 안에 써도 위에꺼랑 같음.

babel 통해서 변역?될 때 위에처럼 코드가 자동으로 바뀜.

그래서 위처럼 constructor 쓰면서 코드 늘릴이유 없음!!! 



css 설정할때 component 최상위 html태그의 className은 snake case로 component 이름을 적어두면 나중에 좋음.

ex) SeasonDisplay.js 이라면

```jsx
<div className={`season-display ${season}`}>
```

이렇게 시작!



children component에서 props를 통해서 인자?를 받는데, 만약 깜빡하고 안넘겨주면? 그럴수도 있겠지! 아니면 특이사항이 없을수도 있고! 그럴때를 대비해서 default값을 설정해둘 수 있음. function parameter 기본값 설정하는거랑 비슷하다고 볼 수 있겠군.

component.js 파일 안에 이렇게!!

```js
import React from 'react';

const Spinner = (props) => {
  return (
    <div className="ui active dimmer">
      <div className="ui big text loader">{props.message}</div>
    </div>
  );
};

Spinner.defaultProps = {
  message: 'Loading...'
}

export default Spinner;
```



**render() 함수에서 return 시킬때는 안에 if문 같은거 쓰지마!!** multiple return statement 안된다!!!

나중에 전체에 적용해야 하는 수정사항이 발생하면 수정하기 귀찮음.

if문을 다른 함수에 넣고 그 함수를 render의 return에서 실행시키렴.

render의 return에는 항상 심플하게!

```js
renderContent() {
    if (this.state.errorMessage && !this.state.lat) {
      return <div>Error: {this.state.errorMessage}</div>;
    }

    if (!this.state.errorMessage && this.state.lat) {
      return <SeasonDisplay lat={this.state.lat} />;
    }

    return <Spinner />;
  }

  render() {
    return (
      <div className="border red">
        {this.renderContent()}
      </div>
    );
  }
```

