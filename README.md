# 리액트 강의 노트

## 기초적인 리액트(첫번째 섹션)

1. React - 엔진과 같다. 인터랙티브한 UI를 만들 수 있도록 도와준다.
2. React-dom - React 요소들을 HTML안에 넣을 수 있게 도와준다.
3. 기존 바닐라JS에서는 HTMl을 먼저 만들고 그걸 자바스크립트로 가져와서 HTMl을 수정했다.
4. 리액트에서는 모든 것이 자바스크립트로 시작해서 HTML로 번역해서 사용한다.
5. 리액트에서는 태그의 property안에 event listner를 등록할수있다.
   1. onClick : ()=>console.log(`name`)
6. 위의 5번 사항에서의 내용으로 리액트는 Property안에 event를 등록하는 장점을 갖는다.
7. 리액트에서는 더 쉽게 사용하기 위해 자바스크립트를 확장한 JSX 문법을 사용한다.
8. 리액트를 쓴다면 다들 사용하는것이 보이는 밑의 코드 사용법과 같다.
   1. const Title = <h3 id="title" onMouseEnter:{()=>console.log("hi")}></h3>
   2. 원시적인 구조는 const Title = React.createElement("tag",{props},content)
9. 위의 JSX는 브라우저가 이해할수 없다. 원시적인 구조의 리액트코드를 이해할수 있다.
   그러므로 babel을 사용해서 JSX를 원시적인 구조로 컴파일해서 브라우저에게 알려줘야한다.
10. 그리고 바벨은 내가 적어놓은 script를 text로 변경하여 head로 올린다.
11. JSX는 각 Components를 모듈화 하여 스택처럼 쌓아 렌더링 할수있다.
12. 11번 말인 즉슨, 컴포넌트를 관리/수정하기가 용이하다(리액트 장점)
13. 리액트 컴포넌트는 첫글자를 대문자로 해야한다. 소문자인 경우 JSX는 단순한 html tag로 인식한다.
14. 화살표 함수는 이전의 함수 선언에서 괄호뒤 return을 써야하는것을 줄이는 장점이 있다.

## STATE (두번째 섹션)

1. state는 기본적으로 데이터가 저장되는 곳
2. 바닐라 자바스크립트에서는 innerText등을 함수에 넣어서 Content를 제어했지만,
   리액트에서는 Content란에 함수를 전달해서 바로 콘텐츠를 제어할수 있다.
   1. span.innerText="hi" -> <span>my nameis {hi}<span>
   2. 그리고 태그 안에 props로 onClick이벤트를 전달하면 리액트의 장점 발휘
3. 하지만 2번의 방법만으론 UI업데이트가 일어나지 않는다. (보통 ReactDom에 root라는 div태그를 한번 실행하기 때문)
   따라서 root에 담긴 자신이 만든 components 등은 로딩 될때 한번만 띄워주고 더이상 렌더를 하지 않는다.
4. 바닐라 자바스크립트에선 바뀐요소가 있으면 부모 엘리멘트까지 업데이트가 되는데,
   리액트에서는 바뀐요소만 업데이트된다. (이벤트버블링 방지)
5. 본격적인 useState Hook은 앞서서 바뀐 요소에 대한 렌더링을 다시 할수 있도록 도와준다.
   1. const 변수 = React.useState() 로 선언하며, 저 변수를 찍어보면 [undefined, function]의 배열로 나온다.
   2. 위 구조에서 undefined는 data고(초기값) function은 data를 바꿀때 사용하는 함수다.
6. State를 짧게 쓰기위해서 배열 사용법에서 const food = [1,2,3] 이것을
   1. 어려운방법 - const a = food[0], const b = food[1], const c = food[2]
   2. 쉬운방법 - const [a,b,c] = food 이렇게 사용한다 --- (사람들이 쓰는 기본적인 useState사용법)
7. 위에 내용 정리 - state에서 변화가 감지되면 재렌더링이 일어난다.
8. 위의 useState의 두번째 인자, 즉 function은 setData와 같이 쓰이고,
   또 화살표 함수를 써서 setData((current)=>current+1)와 같이 data를 current로 바꿔 쓸수있다(더 안전함)
9. JSX에서는 기존 html props 타입 이름을 다르게 하는게 있다.
   1. ex) for, class... => htmlFor, className
10. property중 onChange는 input등의 입력에서 변화를 감지한다.
11. 정확한 input 입력값을 알고싶으면 onChange에 넣을 함수에 event를 생성자로 두고 감지하면 된다.
    정확히는 event.target.value을 써야한다.
12. 그래서 input값을 위의 data에 넣고 싶으면 setData(event.target.value)를 하면 된다.
13. useState 사용 방법중, data에 false를 넣고 setData에 boolean을 줘서 변경할수있다.
    1. ex) const onFlip = () => setFlipped((current)=>!current)
14. 위의 방법으로 두가지 다른 state를 제어할때 props속성에 조건문을 작성할수있다.
    1. 첫번째 state(disbled={flipped===true}) 두번째 state(disabled={flipped===false})
15. 만약 두번째 value가 첫번째 value에 영향을 받는 경우
    1. value={flipped ? minutes : Math.round(minutes/60)} 이렇게 삼항연산자를 사용해서 boolean을 쓸수있다.
    2. 위의 3항 연산자는 flipped===true일때 minutes를 보이고, flipped=false일때는 뒤의 함수를 보여준다.
