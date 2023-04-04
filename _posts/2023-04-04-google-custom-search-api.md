---
layout: single
title: 맨체스터 시티 정보 사이트 만들기 - Google Custom Search API 사용하기
Categories: Solo_Project
tags: [project]
---

<br/>

파이널 프로젝트(팀 프로젝트)가 끝나고 그동안 만들어보고 싶었던 맨시티 관련 웹 사이트를 만들기 시작했다.<br/>
일단 가볍게 홈, 선수 리스트, 맨시티 관련 뉴스 카테고리 정도로 페이지를 만들었는데,<br/>
원래 뉴스 페이지에서 네이버 뉴스 검색 API를 활용해 만들 예정이었지만 키를 발급받아 구현해보던 와중 CORS 에러가 떠서 알아보니 프론트엔드 측에서의 호출이 막혀있다고 나와있었다.<br/>
해외 무료 뉴스 API도 몇가지 찾아봤지만, 이왕이면 한글 기사들을 주로 검색해오고 싶어서 `Google Custom Search API`를 사용해보기로 했다.

<br/>

# Google Custom Search API

## 프로젝트 생성 및 API key 발급

검색 API 관련 정보는 [공식 문서](https://developers.google.com/custom-search/v1/overview?hl=ko)를 보고 단계대로 따랐다.<br/>
[구글 클라우드](https://cloud.google.com/?hl=ko)의 콘솔에서 프로젝트를 생성하고, <br/>
[이 페이지](https://developers.google.com/custom-search/v1/overview?hl=ko)에서 키 가져오기 버튼을 눌러 위에서 만든 프로젝트 선택 후 API key를 발급받았다.

## 검색 엔진 만들기

해당 API는 `Custom Search` API이기 때문에 내가 검색 엔진을 만들어 설정해야 한다.<br/>
[제어판](https://programmablesearchengine.google.com/controlpanel/all)에서 검색 엔진을 만들고, API 호출에 필요한 검색 엔진 ID를 발급 받는다.

## 뉴스 정보를 가져오기 위한 설정

![](/images/2023-04-04-google-custom-search-api/1.png)

위 단계에서 만든 검색 엔진 설정에서 전체 웹에 대해 검색할 것인지, 원하는 사이트에서만 검색할 것인지 정할 수 있다.<br/>
나는 다른 정보들 말고 뉴스 기사만 가져오길 원하기 때문에, 검색 할 사이트에 구글 뉴스 페이지 주소(`news.google.com/*`)를 설정 해주었다.

## React에서 요청 보내기

요청을 위한 필수 파라미터는 `key(첫 단계에 발급받은 API key)`, `cx(생성한 검색엔진 ID)`, `q(검색어)`가 있다.<br/>
다른 파라미터들은 [해당 페이지](https://developers.google.com/custom-search/v1/reference/rest/v1/cse/list?hl=ko)를 참고해 필요한 것들만 추가해주었다.

```typescript
const params: ReqParams = {
  key: process.env.REACT_APP_GOOGLE_API_KEY,
  cx: process.env.REACT_APP_GOOGLE_SEARCH_CX,
  q: "맨시티",
  dateRestrict: "w2",
  hq: "맨체스터 시티",
  start: contentCount,
};
```

내가 구현할 페이지는 맨시티에 관련된 최근 뉴스 기사들을 보여줄 용도였기 때문에, `dateRestrict`를 `w2`로 설정해 최근 2주간의 결과만 가져오도록 설정해주었다.<br/>
또 `hq`를 사용해 맨시티 말고도 맨체스터 시티라는 키워드를 하나 더 추가해 주었다.<br/>
그리고 나는 데이터를 더보기 버튼 형식으로 추가적으로 더 불러오는 기능을 사용해 구현할 것이기 때문에 페이지 관련 정보를 보내야 했는데,<br/>
[해당 페이지](https://developers.google.com/custom-search/v1/reference/rest/v1/cse/list?hl=ko)에는 페이지 파라미터가 아닌 몇번째 데이터부터 보겠다는 형식으로 요청을 보내야 한다고 적혀있어<br/>
contentCount 상태를 만들어 버튼을 누를 때 마다 10씩 더해서 데이터를 불러오는 방식으로 구현하고자 위와 같이 작성 했다.

```typescript
const getNewsData = async () => {
  setIsLoading(true);
  const params: ReqParams = {
    key: process.env.REACT_APP_GOOGLE_API_KEY,
    cx: process.env.REACT_APP_GOOGLE_SEARCH_CX,
    q: "맨시티",
    dateRestrict: "w2",
    hq: "맨체스터 시티",
    start: contentCount,
  };
  await axios
    .get("https://www.googleapis.com/customsearch/v1", {
      params,
    })
    .then((res) => {
      console.log(res);
    });
};
```

![](/images/2023-04-04-google-custom-search-api/2.png)

요청을 보내면 이렇게 응답이 잘 온 모습을 확인할 수 있다. 받아온 데이터를 활용해 아래와 같이 화면에 띄워줬다 :)

![](/images/2023-04-04-google-custom-search-api/3.png)
