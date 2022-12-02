---
layout: single
title: TextContent와 innerText, innerHTML
tags: [JavaScript, DOM]
categories: JavaScript
---

<img src='../images/js-thumbnail.png'>


오늘 간단한 웹앱 만들기(계산기) 과제를 수행하며 `textContent` 프로퍼티를 굉장히 많이 사용했다. 그래서 이 `textContent`와 비슷한 기능을 가진 `innerText`, `innerHTML` 이 세가지 프로퍼티의 기능과 특징, 차이점에 대해 블로깅해보려고 한다 🧐

<br />

## textContent 
>`textContent` 프로퍼티는 setter와 getter 모두 존재하는 접근자 프로퍼티로서 요소 노드의 텍스트와 모든 자손 노드의 텍스트를 모두 변경하거나 취득한다.

>요소 노드의 `textContent` 프로퍼티를 참조하면 **요소 노드의 모든 콘텐츠 영역(시작 태그와 종료 태그 사이)내의 모든 텍스트를 반환한다. 이 때 HTML 마크업은 무시된다.**

```html
...
<body>
  <div id="foo">Hello <span>world!</span></div>
</body>
<script>
    //#foo 요소 노드의 텍스트를 모두 취득한다. 이때 HTML 마크업은 무시된다.
    console.log(document.getElementById('foo').textContent); // Hello world!
</script>
...
```
<br />

>**요소 노드의 `textContent` 프로퍼티에 문자열을 할당하면 요소 노드의 모든 자식 노드가 제거되고 할당한 문자열이 텍스트로 추가된다.** 이때 할당한 문자열에 HTML 마크업이 포함되어 있더라도 문자열 그래도 인식되어 텍스트로 취급된다. 즉, **HTML 마크업이 파싱되지 않는다.**

```html
...
<body>
  <div id="foo">Hello world!</div>
</body>
<script>
  document.getElementById('foo').textContent = 'Hi <span>there!</span>';
</script> 
...
```
![](https://velog.velcdn.com/images/jangmi749/post/ec433d2b-ed3a-4ac7-bac4-f1506eda1627/image.png)
>위와 같이 `span`이 태그로 적용되는 것이 아니고 문자열 그대로 `div#foo` 안에 할당된다.

<br /><br />

## innerText
>`textContent` 프로퍼티와 유사한 동작을 하는 프로퍼티이다.

#### 공통점
>`innerText`와 `textContent` 모두 텍스트노드를 추가한다. 결과 또한 동일하다.

>해당 엘리먼트의 텍스트 값을 반환한다. 즉, 둘 다 지정된 요소 노드가 어떤 텍스트를 가지고 있는지 알 수 있다.

#### 차이점
>`textContent`가 더 먼저 만들어지고, 더 빨리 사용되었다. 앞의 이유로 브라우저 호환성이 좀 더 높고, 큰 차이는 아니지만 더 가볍다고 알려져있다.

>값을 가져올 때 다수의 공백이 존재하는 경우 하나로 가져오느냐, 아니면 모두 그대로 가져오느냐의 차이가 있다.

```html
...
<body>
  <p>Hello     World!</p>
</body>
<script>
  var innet_text = document.querySelector('p').innerText;
  var text_content = document.querySelector('p').textContent;
  
  console.log(inner_text); // Hello World!
  console.lod(text_content); // Hello     World!
</script>
```

<br />

#### innerText 프로퍼티는 다음과 같은 이유로 권장하지 않는다.
>`innerText` 프로퍼티는 CSS에 순종적이다. 예를 들어, CSS에 의해 비표시(`visibility: hidden;`)로 지정된 요소 노드의 텍스트를 반환하지 않는다.

>`innerText` 프로퍼티는 CSS를 고려해야 하므로 `textContent` 프로퍼티보다 느리다.


<br /><br />

## innerHTML
>`innerHTML` 프로퍼티는 setter와 getter 모두 존재하는 접근자 프로퍼티로서 요소 노드의 HTML 마크업을 취득하거나 변경한다. **요소 노드의 innerHTML 프로퍼티를 참조하면 요소 노드의 콘텐츠 영역(시작 태그와 종료 태그 사이) 내에 포함된 모든 HTML 마크업을 문자열로 반환한다.**

```html
...
<body>
  <div id="foo">Hello <span>world!</span></div>
</body>
<script>
  console.log(document.getElementById('foo').innerHTML); // "Hello <span>world!</span>"
</script>
```
```html
<body>
  <div id="foo2">Hi   there!<span style="display:none">hidden text</span></div>
</body>
<script>
  console.log(document.getElementById('foo2').innerHTML
  // "Hi   there!<span style-"display:none">hidden text</span></div>"
</script>
```

>앞서 살펴본 `textContent` 프로퍼티를 참조하면 HTML 마크업을 무시하고 텍스트만 반환하지만, **`innerHTML` 프로퍼티는 HTML 마크업이 포함된 문자열을 그대로 반환한다.**
