---
layout: single
title: \[Pre-Project\] 리액트 파일 절대경로 설정과 eslint 오류
categories: Team_Project
tags: [project, error]
---

<br/>

## 리액트 파일 절대경로 설정 (jsconfig.json)

개인적으로 리액트 프로젝트를 진행할 때 절대경로 설정을 하는 것을 선호하는 편이다. 나중에 폴더를 많이 만들다 보면 경로가 지저분해 지는 것을 별로 좋아하지 않기 때문이다.<br/>

내가 주로 사용하는 방법은 `jsconfig.json`에 루트 디렉터리를 수정하는 방법이다.<br/>
최상위 폴더 안에 `jsconfig.json`(typescript의 경우 `tsconfig.json`)을 생성한 후 아래 코드를 추가한다.

```json
{
  "compilerOptions": {
    "baseUrl": "src"
  }
}
```

이렇게 절대경로 설정을 해주면 아래와 같이 import시 경로 앞의 `../`을 생략할 수 있어 파일 경로의 가독성이 좋아진다.

```javascript
import Comments from "../../components/Comments"; // 상대경로
import Comments from "components/Comments"; // 절대경로
```

## ESLint 오류 발생

위와 같이 파일 절대경로 설정을 해주니 프로젝트 시작 시 지정해놓았던 eslint 규칙에 반하는지 import 관련 오류가 발생했다.<br/>
구글링 후 아래 코드를 `.eslintrc.json`에 추가해주니 오류가 사라졌다 😀

```json
"settings": {
    "import/resolver": {
      "node": {
        "paths": ["src"],
        "extensions": [".js", ".jsx", ".ts", ".tsx"]
      }
    }
  }
```
