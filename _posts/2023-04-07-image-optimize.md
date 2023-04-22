---
layout: single
title: 포트폴리오 사이트 만들기 - avif, webp로 이미지 최적화하기 (feat. lighthouse)
categories: Solo_Project
tags: [project, optimization]
toc: true
toc_sticky: true
---

<br/>

## 이미지 로딩이 너무 느려..! 🤯

그저께부터 만들기 시작했던 포트폴리오 사이트 개발을 1차적으로 마치고 배포를 완료했다.<br/>
그런데.. 프로젝트들을 모아서 보여주는 페이지에 이미지가 들어가 만들 때부터 걱정했는데 역시 배포 링크에 들어가보니 이미지들이 상당히 느리게 나타나서 보기 좋지 않았다 🥲<br/>

![](/images/2023-04-07-image-optimize/1.png)

아무래도 포트폴리오 사이트인데 누군가 들어왔을때 이미지가 느리게 로딩되는걸 원치 않아서 부랴부랴 lighthouse 돌려보기 🙃

## lighthouse

![](/images/2023-04-07-image-optimize/2.png)

예상했던 결과^^.. 프로젝트 배포화면을 캡쳐본 그대로 올려놔서 이미지 사이즈도 어마어마 했고 확장자도 `png` 하나뿐이었으니..<br/>
그래서 저 새빨간 친구들을 빨리 수정해줘야만 했다.

## Properly size images (적절한 사이즈의 이미지를 사용하자)

위에서 말했던대로 나는 배포화면을 캡처했던 이미지를 그대로 사용했기 때문에, 이미지 사이즈가 엄청나게 컸다.<br/>
그런데 이미지 사용은 거의 썸네일정도의 크기로만 사용해서 투머치한 사이즈였기 때문에 이미지 크기를 모두 너비 400px로 맞추어 줄여주었다.<br/>

## Serve images in next-gen formats (차세대 형식 이미지를 제공하자)

`webp`, `avif`는 기존의 `jpeg`, `png` 이미지 포맷보다 압축률이 뛰어나기 때문에 해당 포맷의 이미지를 제공하는것을 지향한다고 한다.<br/>
그래서 가지고 있던 이미지를 `webp`, `avif` 형식으로 변환해 보았다.

![png](/images/2023-04-07-image-optimize/3.png)

![webp](/images/2023-04-07-image-optimize/4.png)

![avif](/images/2023-04-07-image-optimize/5.png)

`webp`도 많이 줄어들었지만 진짜 엄청 압축된 `avif`...<br/>
당연히 `avif`, `webp`를 쓰는게 좋고 대부분의 최신 브라우저들에서는 거의 지원한다고 하지만 지원하지 않는 브라우저도 아직 존재하기 때문에, `<picture>` 태그를 사용해 여러 포맷의 이미지를 제공해 주는 것이 좋다.

```tsx
<div className="project-thumbnail">
  <img className="project-thumbnail-img" src={"이미지주소.png"} />
</div>
```

원래 `png` 포맷의 이미지만 가지고 페이지를 구현했으니 내가 구현해놓은 코드는 img태그 하나만 가지고있었다.<br/>
이제 `avif`, `webp` 포맷의 이미지도 추가했으니, 두 형식도 추가하여 제공하도록 코드를 변경해보자!!

```tsx
<div className="project-thumbnail">
  <picture className="project-thumbnail-img">
    <source srcSet={`/images/avif/${imageSrc}.avif`} type="image/avif" />
    <source srcSet={`/images/webp/${imageSrc}.webp`} type="image/webp" />
    <img src={`/images/png/${imageSrc}.png`} />
  </picture>
</div>
```

`<picture>` 태그는 `<img>` 요소의 다중 이미지 리소스를 위한 컨테이너를 정의할 때 사용된다ㄴ고 한다.<br/>
`<source>` 태그를 이용하여 위에서부터 최적의 이미지 포맷 파일을 순서대로 넣어주고, 가장 마지막에 지원할 포맷을 `<img>`태그 안에 넣어주면 된다.
<br/>

속성에 `media="(max-width: ~~ or ,in-width: ~~)`를 추가해주면 브라우저 크기에 따라 최적화도 가능하다고 한다.<br/>
하지만 나는 이미지를 썸네일 정도의 크기로만 제공해 모든 브라우저에서 이미지 크기 차이가 크지 않기 때문에 이 부분은 생략해주었다.
<br/>

이렇게 `<picture>`, `<source>` 태그를 사용해 여러개의 포맷을 제공하면, 브라우저가 지원하는 포맷의 이미지를 다운로드해서 표시한다고 한다 🧐

![](/images/2023-04-07-image-optimize/6.png)

`avif`를 지원하는 크롬 개발자도구에서 이미지를 확인해보니 `avif` 포맷으로 이미지가 제공되고 있는 것을 확인할 수 있다!

## 수정한 후 다시 lighthouse!

![](/images/2023-04-07-image-optimize/7.png)
(이미지를 수정하며 메인 색상도 함께 수정했습니다)

색상 수정 외에는 이미지 최적화밖에 한게 없는데 점수가 급상승했다...!? 🤯 <br/>
물론 계속 돌려보니 조금 왔다갔다는 하는 것 같지만 일단 이미지 로딩에 관한 메세지는 확실하게 사라진 걸 확인할 수 있었다!

<br/>

자 이제 시연 영상 비디오 파일 최적화하러 가보자.. 총총... 🤣

## Reference

- [lighthouse를 이용해 성능 최적화 하기](https://kyounghwan01.github.io/blog/React/optimize-performance/properly-size-images/#%E1%84%8B%E1%85%AF%E1%86%AB%E1%84%8B%E1%85%B5%E1%86%AB)
- [브라우저 이미지 최적화하기 - WebP - AVIF - JPEG](https://gusrb3164.github.io/web/2021/11/26/browser-image-optimzing/)
- [avif와 webp 포맷을 사용하여 이미지 최적화하기](https://dev-yakuza.posstree.com/ko/web/optimization_images/)
