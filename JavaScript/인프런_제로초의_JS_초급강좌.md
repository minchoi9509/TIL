## 웹 게임을 만들며 배우는 자바스크립트

### :fire: 웹 화면 구현
#### window 객체 
__window__ : 브라우저를 담당하는 객체, window는 생략 가능. 전역 객체.     
__document__ / window.document = window['document'] : 화면, 페이지(탭)을 담당하는 객체   

#### document 객체와 DOM
document : html과 javascript 사이에서 통역사가 되어주는 객체   
__DOM 모델__ : Document Object Model. 

#### JS로 HTML 태그 만들기

* javascript
``` javascript
var  body = document.body;
var  word = document.createElement('div');
word.textContent = '제로초';
var  enter = document.createElement('input');
document.body.append(enter);
var  btn = document.createElement('button');
btn.textContent = '입력';
document.body.append(btn);
var  result = document.createElement('div');
document.body.append(result);
```
* html 
```html
<!DOCTYPE  html>
<html>
<head>
<meta  charset="utf-8"  />
<title>끝말잇기</title>
</head>

<body>
<input  type = "text"  />
<button>등록</button>
<script  src="끝말잇기.js"></script>
</body>
</html>
```

#### 끝말잇기 화면에 표시하기
* ver 1. 
```javascript
btn.addEventListener('click', function() {

if(word.textContent[word.textContent.length - 1] == enter.value[0]) {
result.textContent = '딩동댕';
word.textContent = enter.value;
enter.value = '';
}else {
result.textContent = '땡';
}

});
```

* ver 2. form으로 제출하기
``` javascript
var  body = document.body;
var  word = document.createElement('div');
word.textContent = '제로초';
document.body.append(word);
var  form = document.createElement('form');
document.body.append(form);
var  enter = document.createElement('input');
form.append(enter);
var  btn = document.createElement('button');
btn.textContent = '입력';
form.append(btn);
var  result = document.createElement('div');
document.body.append(result);

form.addEventListener('submit', function(e) {

e.preventDefault();

if(word.textContent[word.textContent.length - 1] == enter.value[0]) {
result.textContent = '딩동댕';
word.textContent = enter.value;
enter.value = '';
enter.focus();

}else {

result.textContent = '땡';
enter.value = '';
enter.focus();

}

});
```

form을 submit 한다는 건 제출되면서 새로고침이 된다는 의미임. 하지만 브라우저에서 새로고침이 되는 경우 내용들이 다 날라가기 때문에 `e.preventDefault()` 이 메소드를 통해서 새로고침을 방지 함. 

#### 비동기 & 숫자야구 순서도
* 자바스크립트에서 비동기는 코드 상의 순서대로 실행되지 않는 코드 > 콜백함수  
* 공통적인 것은 배열로 묶어주는 것이 좋음

.pop() 배열 뒤에서부터 하나씩  뽑는 것
.shift() 배열 앞에서부터 하나씩 뽑는 것
: 뽑아서 그 배열에서 사라짐  
<->   
.push() 배열 차례대로 넣는 것 1, 2, 3, 4
.unshift() 4, 3, 2, 1   

배열에서 랜덤하게 뽑고 싶은 경우 : `splice(Math.floor(Math.random() * (9 - i)), 1)[0]`

배열.join('') > 배열이 하나의 문자열로 합쳐지게하는 메소드  
문자.split(''); > 문자열을 배열로 만들고 싶은 경우 사용하는 메소드

배열.indexOf(); > 배열 안에서 몇 번 째에 있는지 알 수있는 메소드.  존재하지 않으면 -1.   

Number(배열[i]) : 배열의 자료형이 number라고 명시해줌.  
