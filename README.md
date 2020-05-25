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
=> ex)<Food name="kimchi" /> Food component에 kimchi라는 value로 prop name을 줬다.
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

#4.0 Fetching Movies from API
일반적으로 사람들이 javascript에서 data를 fetch하는 방법은 fetch API를 사용하는 것.
하지만 더 좋은 방법으로 Axios가 있음. axios.get()은 항상 빠르지 않기 때문에 자바스크립트에게
작업이 끝날때까지 기다려달라고 요청해야함. 이 때, async와 await을 이용하여 설정(비동기)

※application은 Render한다 -> 처음에는 isLoading : true -> application이 mount된 후 getMovies function 호출
-> getMovies는 axios.get()을 사용. 하지만 axios.get은 완료되기까지 시간이 필요하기 때문에 앞에 await 첨부
(이때 async를 사용하지 않으면 await 키워드도 사용 불가)

#4.1 Rendering the Movies
const movies.data.data.movies => ES6 ver. const {data : {data : { movies }}}로 고칠 수 있음. 따라서 사용할때는 그냥 movies로 사용가능
this.setState(movies(state안의 movies[]) : movies(현재 axios로 가져온 데이터)) => this.setState(movies)로 고쳐서 사용해도 됨
is loading : false 일때 movies.map()을 사용하여 원하는 Props를 가져온 뒤 Movie Component를 Rendering

#4.2 Styling the Movies
jsx는 html이 아니기 때문에 태그의 class를 설정할 때는 className으로 정의해야 한다.(javascript class와 충돌 가능성이 있기 때문)
EX)<label for> -> <label htmlFor>
만약 style을 주고싶으면 style={{backgroundColor:"red"}} 형태로 사용한다.(javascript 형태의 CSS)
하지만 따로 css파일을 만들어 import해서 사용할 것을 권장

#4.3 Adding Genres
props에 array를 포함시킬 때 genres: PropTypes.arrayOf(PropTypes.string).isRequired 형태로 써야한다.
