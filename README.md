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

#5.0 Deploying to Github Pages

- 코드를 cloud에 올리는 법(github page)

1. gh-pages 설치(npm install gh-pages) > github에 업로드하는 것을 허가해주는 모듈로써 나의 웹사이트를 github의 github page 도메인에 나타나게 해줌
   (무료로 static , HTML, Css, Javvascript 웹사이트를 제공함)
2. package.JSON 으로 가서 homepage를 추가
   "homepage" : "username(zgeniez).github.io/project name(movie_app)"
   ※이때 username과 project name은 모두 lowercase여야 함
3. npm run build 명령으로 build폴더를 만들고, script에 deploy,predeploy 추가하기
   "deploy" : "gh-pages -d build" <- 이때 폴더이름과 build이 같아야 함
   "predeploy" : "npm run build" <- deploy 명령어를 입력할 때마다 실행되기 전에 자동으로 predeploy가 실행. pre를 붙일때에는 이름 형식이 같아야 자동으로 실행됨

#5.1 Are we done
더 이상 state를 갖기 위해 class component를 가질 필요가 없음 . WHY ? React Hook을 사용하면 됨!
react hook은 새로운 것이고 대체물은 아님. (class component가 구식이 아님)

#6.0 Getting Ready for the Router
페이지에 인터랙션을 더 추가하기(네비게이션바)
React-router-dom이란 ? 네비게이션을 만들어주는 패키지(npm install react-router-dom으로 설치)
2개의 라우터로 구성하여 2개의 스크린을 만듬(영화 설명(홈),about페이지)
App.js에 있는 내용을 모두 Home.js로 옮기고 App.js에는 라우터 추가

#6.1 Building the Router
App.js에 Router를 반환함으로써 Home.js로 가거나 About.js로 가게 만듬
HashRouter, Route를 import 하여 사용.
이때 Route 안에는 매우 중요한 props가 들어감(렌더링할 스크린,다른 prop은 뭘 할지 정해줌)
props중 path에는 경로, component에는 보여줄 컴포넌트를 넣어줌
※path가 /,/about 같이 겹치는 경로가 존재할 경우 리액트 라우터가 작동하는 방식(기본적으로 url을 가져와 라우터에서 비교함.처음에는 /가 매치되고 그다음에는 /about이 매치되어 /가 라우트로 여겨짐.따라서 동시에 렌더링) 때문에 2개의 컴포넌트가 동시에 렌더링됨.

- 해결방법 : 첫번째 route의 props에 exact = {true}를 추가해준다.위의 예제에는 /의 props에 추가해주면 되는데 이때 리액트 라우터는 url이 /일때만 home을 렌더링해준다.

#6.2 Building the Navigation
네비게이션 컴포넌트를 추가한다. 이때 a href를 사용하여 home,about을 누르면 페이지가 새로고침되버림(html 특성)
따라서 react-router-dom에 있는 Link를 import해서 사용.
※Router 밖에서는 Link를 사용할 수 없다. HashRouter 대신에 BrowserRouter를 쓰면 주소창의 /#/이 사라진다.
하지만 github pages에 정확히 설정하기 어렵기 때문에 HashRouter로 하는게 쉬움

#6.3 Sharing Props Between Routes
route props
모든 컴포넌트에는 props가 존재함. ex)movie.js에서는 {year,title,...} 과 같은 props를 보내고 있음
about.js에서 console.log(props)를 하면 history,location,match,staticContent과 같은 4개의 props가 존재함
이것들은 아직 about으로 전송되지 않았음. (react-router에 의해서 넣어짐)
※라우터에 있는 모든 라우트들은 기본값으로 props를 가짐 <- movie를 클릭하면 Detail 페이지에 props를 전달
Link to의 값을 string -> object로 변경하여 보낼 수 있음 ex)<Link to={{pathname:"/about", state:{fromNavigation:true}}}>
링크를 클릭하면 리액트 라우터는 pathname으로 데려가고 route로 props도 전달해줌.

#6.4 Redirecting
링크를 통해 정보를 라우터로 보내고 있음. 현재 전달한 정보는 props -> location -> state안에 존재.
이 때 movie를 클릭하지 않고 주소창에 /movie-detail을 치면 state에는 아무것도 존재하지 않음.(movie를 클릭해야
해당 props가 전달되기 때문) 따라서 class 컴포넌트로 핸들링.
componentDidMount()에 location.state가 존재하지 않으면(undefined) 홈으로 리다이렉트 (props의 history.push()사용) 따라서 movie를 직접적으로 클릭해야 detail 페이지로 가고 나머지 경우는 모두 홈으로 리다이렉트 시킴.
하지만 한번 render() 후에 주소창에 /movie-detail을 치면 location이 더이상 존재하지 않기 때문에 오류가 발생한다.
(render()가 실행되고 componentDidMount()가 실행되기 때문에 componentDidMount안의 에러 핸들링이 실행될 수 없음)
해결법으로 location.state가 존재하지 않을 시 null을 반환하는 것으로 오류를 해결. 이로써 link를 사용하여 스크린사이에서 정보를 공유할 수 있음. 네비게이션은 이런 Props가 존재하지 않음.오직 Route에서만 !
path에 변수(id)로 주소를 지정하고 싶다면 App.js의 link path="/movie/:id"로 고치고 Movie.js의 link to="pathname=`/movie/${id}`로 고친다.

#6.5 Conclusions
home -> about -> home으로 가면 다시 로딩된 후 화면이 뜬다. 왜? home에 state가 갇혀있기 때문!
그래서 매번 home이 사라지면 (about을 클릭했다면) 다시 home을 가면 state가 비어있게 된다. (데이터를 다시 불러와야되기 때문) <- 효율성 떨어짐
따라서 redux를 쓰면 state를 스크린 밖에 있도록 해준다.(데이터를 매번 불러올 필요가 없다.왜? state를 저장하기 떄문에)
