## CSS MASTER CLASS

block: 한칸을 무조건 차지
inline: 텍스트와 같이 컨텐츠만의 크기를 가짐(div만 만들면 자리 차지 안해서 암것도 안보임)
inline-block: div의 실제 크기만큼의 크기를 가짐

#### flex

##### 부모 컨테이너에 적용되는 속성

```css
.father {
  display: flex;
  row-gap: 10px;
  column-gap: 20px;
  justify-content: center;
  align-items: center;
  flex-flow: row wrap;
  align-content: center;
}
```

##### 자식 개체에게 적용되는 속성

```css
.child {
  align-self: flex-start;
  align-self: flex-end;
  order: 1; /*기본적으로 0 */
}
```

컨태이너의 자식들에게 차지할 크기를 지정 -> flex-grow
`flex-frow: 1;` //1의 비율 만큼 크기를 차지함

컨테이너 자식들에게 최대 얼마나 줄어들지 지정 -> flex-shrink
`flex-shrink: 3;`
//이 속성을 가진 자식개체가 뒤에서 3번째로 빨리 줄어듦, 0이면 객체의 컨텐츠보다 작아지지 않음

초기 시작 크기를 지정 -> flex-basis
`flex-basis: 500px;` //기본 크기를 500px로 지정

`flex: <grow> <shrink> <basis>;` //다음과 같이 단축 가능

#### Grid

```css
.father {
  display: grid;
  grid-template-columns: 100px [lineName] 200px 50px;
  grid-template-rows: 200px 100px;
  row-gap: 10px;
  column-gap: 20px;
}

.child {
  background-color: tomato;
  display: flex;
  color: white;
  font-size: 28px;
  align-items: center;
  justify-content: center;
}

.child:last-child {
  background-color: turquoise;
  grid-column: lineName / span 2; /*[potato]부터 셀을 열로 두 칸 차지 */
  /*
  grid-column-start: 2;
  grid-column-end: -1; 
  */
}

.child:first-child {
  grid-row-start: 1;
  grid-row-end: -1;
  grid-row: span 2;
  background-color: khaki;
}
```

```css
body {
  padding: 0;
  margin: 0;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;

  display: grid;
  height: 100vh;
  /* grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr 2fr 1fr;
  grid-template-areas:
    "a a a a"
    "b b b c"
    "d d d d"; */

  grid-template:
    "a a a a" 1fr
    "b b b c" 2fr
    "d d d d" 1fr / 1fr 1fr 1fr 1fr;
}

header {
  background-color: aqua;
  grid-area: a; /*템플릿 이름 지정*/
}

section {
  background-color: coral;
  grid-area: b;
}

aside {
  background-color: forestgreen;
  grid-area: c;
}

footer {
  background-color: deeppink;
  grid-area: d;
}
```

```css
.father {
  display: grid;
  gap: 10px;
  min-height: 50vh;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(2, 1fr);
  grid-auto-rows: 1fr; /*지정된 행보다 늘어났을 때 지정한 크기*/
  grid-auto-columns: 1fr; /*지정된 행보다 늘어났을 때 지정한 크기*/
  grid-auto-flow: column; /*지정된 행,열을 넘었을 때 기준을 열로 바꿈*/
  place-items: end center; /*자식 개체들의 <행 열> 의 위치 지정 */
}

.child:nth-child(6) {
  background-color: teal;
  /* align-self: start;
  justify-self: end; */
  place-self: center center; /*해당 객체 하나의 위치만 조정*/
  grid-column: span 2;
}
```

```css
.father {
  display: grid;
  gap: 10px;
  height: 100vh;
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: repeat(2, 100px);
  background-color: lightblue;
  /*
  justify-content: start;
  align-content: end;
  */
  place-content: start end; /*그리드 안의 행과 열의 위치관계를 지정*/
}
```

```css
.father {
  display: grid;
  gap: 10px;
  grid-template-rows: 1fr max-content min-content 1fr;
  /*max는 콘텐츠보다 안줄어들고 min은 최소 컨텐츠만큼 줄어듦 */
  grid-template-columns: repeat(3, minmax(300px, 350px));
}
```

```css
.father {
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  /*auto-fit: 빈 공간 없이 배열됨,  auto-fill: 빈 공간이 생기면 빈 그리드를 생성해서 채운다 */
}
```

#### SCSS

npm add -D sass

```scss
$varName: red;

body {
  background-color: $varName;
}
```

- nesting: 반복을 줄이기 위한 문법, 부모태그에 속한 자식태그를 괄호 안에 넣어서 구분

```scss
ul {
  list-style-type: none;
  padding: 0;
  display: flex;
  gap: 10px;
  li {
    background-color: tomato;
    color: white;
    padding: 5px 10px;
    border-radius: 7px;
    &:hover {
      /*li:hover */
      opacity: 0.8;
      a {
        color: gray;
      }
    }

    a {
      text-decoration: none;
      color: white;
      text-transform: uppercase;
    }
  }
}
```

- @extend

```scss
%styleName { /*부모 클래스와 같은 역할 */
  ...
}

.child1 {
  @extend %styleName; /*상속하는 것처럼 styleName에 있는 내용을 상속*/
  background-color: red;
}

.child2 {
  @extend %styleName;
  background-color: blue;
}
```

- @mixin

```scss
@mixin styleName($bgColor, $borderColor) {
  //함수 처럼 인자를 받아 사용할 수 있다
  background-color: $bgColor;
  border: 1px dashed $borderColor;
}

.child1 {
  @include alert(green, blue); //파라미터 전달, 상속
}

.child2 {
  @include alert(yellow, black);
}
```
