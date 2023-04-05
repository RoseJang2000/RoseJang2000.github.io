---
layout: single
title: Single Page Application & React Router
tags: [React, SPA, React Router]
categories: React
toc: true
toc_sticky: true
---

# 🔘 SPA

## 👉 SPA의 등장 배경

전통적인 웹 사이트에서는 사용자가 웹 사이트 내의 다른 페이지로 이동할 때, 브라우저가 페이지를 보여주기 위해 매번 HTML 파일로 된 **페이지 전체**를 불러와야만 했다.

SPA는 Menu와 Footer 등과 같이 페이지 전환 전후에 중복되는 부분은 새로 불러오지 않는다. 전통적인 웹 사이트에서는 “페이지 전체를 불러오는 행위”를 보통 깜빡인다고 표현한다.

웹 사이트가 보다 복잡해지고 앱의 형태를 띄면서, 사용자와 서비스 사이에 더 많은 상호작용이 일어나게 되었다. 이때마다 Header나 Navigation Bar와 같이 중복되는 요소들을 매번 불러오는 것이 트래픽 증가와 사용자 경험의 저하를 야기했다.

1990년대 후반에 HTML 문서 전체가 아니라 업데이트에 필요한 데이터만 받아, JavaScript가 이 데이터를 조작하여 HTML 요소를 생성하여 화면에 보여주는 방식이 개발되었다. 2000년대 중반부터 이런 방식이 보편화 되었으며, 이것이 SPA(Single Page Application)이다.

## 👉 SPA란?

<aside>
💡 서버로부터 완전한 새로운 페이지를 불러오지 않고 페이지 갱신에 필요한 데이터만 받아 그 정보를 기준으로 현재의 페이지를 업데이트 함으로써 사용자와 소통하는 웹 어플리케이션이나 웹 사이트.

</aside>

### 👍 SPA의 장점

- 전체 페이지가 아니라 필요한 부분의 데이터만 받아서 화면을 업데이트 하면 되기 때문에 사용자와의 인터랙션에 빠르게 반응한다.
- 서버에서는 요청받은 데이터만 넘겨주면 되기 때문에 서버 과부하 문제가 현저하게 줄어든다.
- 전체 페이지를 렌더링 할 필요가 없기 때문에 더 나은 유저 경험을 제공한다.
- 대표적인 SPA 방식으로 만들어진 서비스 : `Youtube`, `facebook`, `Gmail`, `aitbnb`, `Nexflix` 등

### 👎 SPA의 단점

- SPA의 경우 JavaScript 파일의 크기가 크다.
  때문에 이 JavaScript 파일을 기다리는 시간으로 인해 첫 화면 로딩 시간이 길어진다.
- 검색 엔진 최적화(SEO)가 좋지 않다. 구글이나 네이버 같은 검색 엔진은 HTML 파일에 있는 자료를 분석하는 방식으로 검색 기능을 구동하는데, SPA의 경우 HTML 파일은 별다른 자료가 없기 때문에 검색 엔진이 적절히 동작하지 못한다.

> ❓ 검색 엔진의 작동 방식

검색 로봇이 웹 페이지에 있는 정보를 수집하고 분석하여 그 결과값에 인덱스를 만들어 보관하고 있다가, 사용자가 검색어를 입력하면 보관하고 있던 인덱스에서 검색어와 가장 연관성이 높은 웹 페이지들을 수서대로 보여주는 방식으로 작동한다.

검색 로봇은 자료를 수집할 때 웹 페이지의 URL, HTML 문서 내의 각종 태그나 링크 들을 분석하는데, SPA는 HTML이 거의 비어있다 보니 검색 로봇이 충분한 자료를 수집하지 못한다.
이 때문에 검색 엔진 최적화에 대한 대응책을 따로 마련해야 한고, 더불에 앱 안에서 브라우저의 앞으로 가기/뒤로 가기 등의 상태도 관리해야 하기 때문에 개발의 복잡도가 더욱 늘어난다.
(다만, SPA에서도 검색 엔진 최적화에 대응할 수 있도록 검색 엔진이 발전하고 있어 이 단점은 점차 사라지고 있는 추세이다.)

>

# 🔘 Routing & React Router

## 👉 Routing?

Twitter와 같은 SPA 페이지를 만들 때, 메인 트윗 모음 페이지, 알림 페이지, 마이 트윗 페이지 등의 화면이 필요할 수 있다.

![001](/images/2022-11-28-react-spa-router/001.png)

이 화면에 따라 **주소**도 달라지게 되는데, 이렇게 \*\*다른 주소에 따라 다른 뷰를 보여주는 과정을 “경로에 따라 변경한다.”라는 의미로 <span style="text-decoration: underline;">라우팅(Routing)</span> 이라고 한다.

## 👉 React Router

![002](/images/2022-11-28-react-spa-router/002.png)

하지만 React 자체에는 이 기능이 내장되어 있지 않아 우리가 직접 주소 마다 다른 뷰를 보여줘야 한다.

React SPA에서는 라우팅을 위해 **React Router**라는 라이브러리를 가장 많이 사용한다.

### ▶️ React Router 주요 컴포넌트

![003](/images/2022-11-28-react-spa-router/003.png)

- <BrowserRouter> → 라우터 역할
- <Routes> → 경로 매칭
- <Route> → 경로 매칭
- <Link> → 경로 변경

### ▶️ React Router 사용

`npm install react-router-dom@ ^6.3.0`

- App.js

`import React from "react";`

`import {BrowserRouter, Routes, Route, Link} from "react-router-dom";`
