# Movie App

React JS Fundamentals Course

#2.0 Creating your first React Component
- React는 Component와 함께 동작. 하며 component를 사용해서 HTML처럼 작성하려는 경우에 필요.
- JSX = javascript와 HTML 사이의 조합
 Component란? HTML을 반환하는 함수. 항상 컴포넌트를 사용할때는 <컴포넌트이름 />형태로 사용해야함. 
- React Application이 한번에 하나의 component만을 rendering 해야하기 때문에 
ReactDOM.render(<APP /><Potato />, document.getElementById("root")); 같은 형식은 불가.

#2.1 Reusable Components with JSX + Props
jsx에서는 component에 정보를 보낼수 있다.
=> ex)<Food name="kimchi" />  Food component에 kimchi라는 value로 prop name을 줬다.
이때 props들은 function Food(props){} 에서 인자로 들어가고 object의 형태로 전달된다. 
위의 kimchi는 {props.name} 또는 function Food({name}){} 에서 {name}의 형태로 사용할 수 있다. 
react의 특징 : 재사용 가능한 component를 만들 수 있다.

#2.2 Dynamic Component Generation
- 웹사이트에 동적데이터를 추가하는 방법
배열을 사용하여 object의 list를 만들고 map()을 사용하여 원하는 방식으로 데이터를 수정

#2.3 map Recap
- 모든 react의 element들은 유일해야 한다. 따라서 prop으로 "key"를 추가하여 각 element들을 유일성을 갖게 할 필요가 있다.

#2.4 Protection with PropTypes
PropTypes
- 부모 Component로 받은 props가 예상한 props인지 확인해주는 기능을 수행
- 설치방법 : npm i prop-types  
- 사용방법  
import PropTypes from "prop-types";

컴포넌트이름.propTypes = {
  prop이름 : PropTypes.형식(string,number...).필수여부(isRequired) => 필수여부를 적어주지 않으면 굳이 prop값을 줄필요가 없음
}

#3.0 Class Components and State
Class Component를 사용하는 이유 : 매번 component를 만들 때마다 모든 것을 다 구현하지 않고 React.Component를
상속받은 클래스를 이용하여 확장하기 위해

※Function Component VS Class Component
1.Function Component는 순수 자바스크립트 함수를 사용한 function이고 반드시 무엇을 리턴하여 스크린에 표시하지만
Class Component는 react Component로부터 확장되어 스크린에 표시(render 사용)
2. react는 자동적으로 모든 class Component의 render method를 실행
3. Class Component가 코드는 길지만 state를 사용하여 setState()를 통해 life-cycle함수를 사용가능

#3.1 All you need to know about State
state는 직접적으로 변경할 수 없다. 반드시 setState()를 통해 변경해야 함 
why? 직접적으로 state를 변경하면 react가 render function을 refresh하지 않기 때문
※매 순간 setState()를 호출할 때마다 react는 새로운 state와 함께 render function을 호출함

#3.2 Component Life Cycle
react component 에서 사용하는 유일한 function -> render function이다. 
하지만 component, react class component는 단순히 render 말고 더 많은걸 가지고 있음
What? 이들은 life cycle method를 가진다. life cycle method는 기본적으로 react가 component를 생성하고 없애는 방법이다.
component가 생성될 때, render된 후,update될 때, 호출되는 function들이 존재함.
※잘 사용하지 않는 function들은 제외하고 적음(React 홈페이지 참고)
1. Mounting(생성될때)
- constructor() : component가 mount될 때, component가 screen에 표시될 때, component가 나의 website에 갈때 호출됨
- render() 
- componentDidMount(): render()후에 component가 생성된 후 호출됨

2. Updating
setState()가 실행될 때마다 호출됨
- render()
- componentDidUpdate() : render()후에 component가 업데이트 된 후 호출됨 

3. Unmounting(사라질때)
- render()
- componentWillUnmount() : render()후에 component가 제거된 후 호출됨
