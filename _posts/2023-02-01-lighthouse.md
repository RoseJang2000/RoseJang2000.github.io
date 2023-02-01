---
layout: single
title: Google Lighthouse
Categories: Web
---

<br/>

perfomance: 웹 성능을 측정.

> **perfomance 측정의 기준이 되는 항목:**<br/>Eliminate render-blocking resources<br/>Properly size images<br/>Defer offscreen images<br/>Minify CSS<br/>Minify JavaScript<br/>Remove unused CSS<br/>Efficiently encode images<br/>Serve images in modern formats<br/>Enable text compression<br/>Preconnect to required origins<br/>Reduce server response times (TTFB)<br/>Avoid multiple page redirects<br/>Preload key requests<br/>Use video formats for animated content<br/>Reduce the impact of third-party code<br/>Avoid non-composited animations<br/>Lazy load third-party resources with facades

<br/>

### Minify CSS

CSS 파일을 축소하여 페이지 로드 성능을 향상시킬 수 있다. <br/>

ex)

```css
//before
h1 {
  background-color: #000000;
}
h2 {
  background-color: #000000;
}
```

```css
//after
h1,
h2 {
  background-color: #000000;
}
```

또한 위 예제와 같은 색상코드는 `#000000` 대신 `#000`으로 한번 더 축약해 사용할 수 있다.

<br/>

### use video formats for animated content

큰 GIF 이미지는 콘텐츠를 전달하는 데 비효율적이기 때문에 비디오로 변환하면 사용자의 대역폭을 크게 절약할 수 있다. 네트워크 바이트를 절약하기 위해 애니메이션에는 MPEF4/WebM 비디오를 사용하고 정적 이미지에는 PNG/WebP를 사용하는 것이 좋다.
<br/>

#### FFmpeg를 사용해 MPEF 비디오 만들기

FFmpeg를 사용하여 GIF `my-animation.gif`를 MP4 비디오로 변환하려면 다음 명령을 실행하면 된다.<br/>

`ffmpeg -i my-animation.gif my-animation.mp4`<br/>

이렇게 하면 FFmpeg가 플래그 `my-animation.gif`로 표시되는 입력 -i을 받아 비디오라는 비디오로 변환하도록 지시한다. `my-animation.mp4`

#### FFmpeg를 사용해 WebM 비디오 만들기

WebM 비디오는 MP4 비디오보다 훨씬 작지만 모든 브라우저가 WebM을 지원하는 것은 아니므로 둘 다 생성하는 것이 좋다.<br/>

FFmpeg를 사용하여 `my-animation.gif`를 WebM 비디오로 변환하려면 다음 명령을 실행하면 된다.<br/>

`ffmpeg -i my-animation.gif -c vp9 -b:v 0 -crf 41 my-animation.webm`

### Minify JavaScript

사용하지 않는 자바스크립트 코드를 삭제하거나 필수적이 아닌 whitespace를 없애는 것은 자바스크립트 코드를 최적화 시키는데 도움을 줄 수 있다. 그리고 최적화된 JavaScript코드는 코드를 parse하는 시간과 payload의 크기를 줄일 수 있다.<br/>

리액트의 경우, npm run build로 코드가 자동으로 최적화 된다면, production 모드로 빌드를 하고 있는지 꼭 확인해야 한다.
