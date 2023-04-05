---
layout: single
title: 번들링과 웹팩
categories: React
tags: []
toc: true
toc_sticky: true
---

<br/>

# 번들링 (Bundling)

## 번들과 번들링

현대 웹 개발에서 프론트엔드 개발자에게 **번들**은 **"사용자에게 웹 애플리케이션을 제공하기 위한 파일 묶음"**을 의미한다. 사용자가 브라우저를 열고 주소를 입력하면, 해당 주소에서 프론트엔드 개발자가 번들링한 여러 파일을 받는다. 이 파일을 브라우저가 실행하여 웹 애플리케이션을 사용자에게 제공한다.

## 번들링의 필요성

번들링을 하지 않고 내가 작성한 HTML, CSS, JavaScript 파일을 그대로 전송한다면 아래와 같은 어려움에 처할 수도 있다.

- 두 개의 .js 파일에서 같은 변수를 사용하고 있어, 변수 간 충돌이 일어난다.
- 딱 한 번 불러오는 프레임워크 코드가 8MB라서, 인터넷 속도가 느린 국가의 모바일 환경에서 사용자가 불편함을 호소한다.
- 번들 파일 사이즈를 줄이기 위해서 파일의 공백을 모두 지웠는데, 가독성이 너무 떨어져 코딩하기 어려울 수 있다. 결국 그대로 공백을 되돌려 코딩한다.
- 배포 코드가 너무 읽기 쉬어 개발을 할 줄 아는 사용자가 프론트엔드 애플리케이션을 임의로 조작하여 피해가 발생한다.

이 중에서 용량이나 조작에 관한 문제는 프론트엔드 개발 뿐만이 아닌 게임에서도 충분히 생길 수 있는 일이다.<br/>

패미컴으로 발매되었던 닌텐도의 유명 게임인 '슈퍼마리오4'는 물리적 한계에 맞추어 게임을 매우 작은 용량으로 줄이기 위해 기존에 만든 그래픽 패턴을 재사용 한다거나, 색 표현 범위를 최소화하는 등 최적화 절차를 거쳐야만 했다. 이런 사례처럼 번들링 작업에서는 필연적으로 용량을 줄이고 파일을 통일하는 툴링 작업이 필요하게 된다. 즉, 소프트웨어를 잘 만들어도 사용자에게 배포하기 위해 번들링이 꼭 필요하다.

<br/>

# 웹팩 (Webpack)

webpack은 현재 프론트엔드 애플리케이션 배포를 위해서 가장 많이 사용하는 번들러이다. 실리콘벨리나 국내 IT 대기업을 막론하고 프론트엔드 애플리케이션을 대규모 유저에게 제공하기 위해 가장 많이 사용하는 방법이다. 많은 웹 개발자에게 사랑받고 있고, 이제는 Node.js 백엔드 개발자도 배포를 위해서 많이 사용한다.

![javascript bundler npm trends](https://s3.ap-northeast-2.amazonaws.com/urclass-images/6oLj-5h6JP_5P-7CciRUI-1658690485689.png)

## Webpack이란

Webpack이란 여러 개의 파일을 하나의 파일로 합쳐주는 모듈 번들러를 의미한다. 모듈 번들러란 HTML, CSS, JavaScript 등의 자원을 전부 각각의 모듈로 보고 이를 조합해 하나의 묶음으로 번들링(빌드)하는 도구이다.

### 모듈 번들러(Module Bundler)의 등장

모던 웹으로 발전하며 자바스크립트 코드의 양이 절대적으로 많이 증가했고, 또 대규모의 의존성 트리를 가지고 있는 대형 웹 애플리케이션이 등장하므로써 세분화된 모듈 파일이 폭발적으로 증가했다. 이 모듈 단위의 파일을들 호출해 브라우저에 띄울 때, 자바스크립트 언어의 특성에 따라 발생하기 쉬운 각 변수들의 스코프 문제들을 해결하고 각 자원을 호출할 때 생겨나는 네트워크 쪽의 코스트도 신경써야 했다.<br/>

이런 복잡성에 대응하기 위해 하나의 시작점(Ex. React App의 index.js)으로부터 의존성을 가지는 모듈을 모두 추적하여 하나의 결과물을 만들어내는 모듈 번들러가 등장하게 되었다.

### Webpack에서의 모듈

Webpack에서의 모듈은 자바스크립트 모듈에만 국한되지 않는다. HTML, CSS 혹은 .jpg나 .png같은 이미지 파일들도 전부 포함한 포괄적인 개념이다.

![](https://s3.ap-northeast-2.amazonaws.com/urclass-images/ss3Vbw5V6m3NnXR3vIYmc-1658690500906.gif)

따라서 Webpack은 주요 구성 요소인 로더(loader)를 통해 다양한 파일도 번들링이 가능하다.

## 빌드와 번들링

빌드는 개발이 완료된 앱을 배포하기 위해 하나의 폴더(directory)로 구성하여 준비하는 작업을 말한다. React 앱을 기준으로, npm run build를 실행하면 React build 작업이 진행되고, index.html 파일에 압축되어 배포에 최적화된 상태를 제공한다.<br/>

번들링은 말 그대로 묶음의 개념이다. 파일을 묶는 작업 그 자체를 말하며 파일은 의존적 관계에 있는 파일들(import, export) 그 자체 혹은 내부적으로 포함 되어 있는 모듈을 의미한다. 정확히 말하면 모듈 간의 의존성 관계를 파악해 그룹화 하는 작업이라고 볼 수 있다.

## Webpack의 필요성

Webpack이 필요한 가장 큰 이유는 웹 애플리케이션의 빠른 로딩 속도와 높은 성능을 위해서이다. 웹 페이지를 구성하는 코드가 무거우면 무거울수록 웹 페이지의 로딩 속도와 성능은 저하가 된다. 일반적으로 유저는 하나의 웹 사이트에 접근하는 순간부터 3초 이내에 웹 페이지가 뜨지 않으면 굉장히 많은 수가 더는 기다리지 않고 이탈을 선택한다.

![](https://s3.ap-northeast-2.amazonaws.com/urclass-images/IXnI86ws2Ei-mcSbm6ze5-1658690514468.png)

그렇기 때문에 로딩 속도를 개선하기 위한 많은 노력이 필요했고, 그 대표적인 것으로 브라우저에서 서버로 요청하는 파일의 숫자를 줄이는 것이었다.<br/>

Webpack이 없다면 각 자원들을 일일히 서버에 요청해 얻어와야 하지만, Webpack이 있다면 같은 타입의 파일들은 묶어서 요청 및 응답을 받을 수 있기 때문에 네트워크 코스트가 획기적으로 줄어든다.<br/>

또한 Webpack loader를 사용하면 일부 브라우저에서 지원하지 않는 자바스크립트 ES6 문법들을 ES5로 변환해주는 babel-loader를 사용할 수 있게 된다. Vue인 경우는 vue-loader를, scss 파일 같은 경우는 css 파일로 변환해주는 scss-loader 등의 loader도 사용할 수 있기 때문에 개발자는 본인이 원하는 최선의 개발 방식을 선택해 개발할 수 있게끔 지원하기도 한다.<br/>

그리고 Webpack4 버전 이상부터는 Develoment, Production 두 가지의 모드를 지원한다. 여기서 Production 모드로 번들링을 진행할 경우, 코드 난독화, 압축, 최적화(Tree Shaking) 작업을 지원하기도 한다. 한마디로 상용화 된 프로그램을 사용자가 느끼기에 더욱 쾌적한 환경 및 보안까지 신경쓰면서 노출시킬 수 있다는 점에서도 Webpack의 필요성은 굉장히 높은 편이라고 할 수 있다.

<br/>

# Webpack의 핵심 개념

웹팩 공식 문서에서는 아래 항목들을 핵심 개념으로 제안하고 있다. 아래 개념에 대해서 제대로 이해하고 있으면, 웹팩의 작동 원리에 대해 더 쉽게 이해할 수 있다.

- Entry
- Output
- Loaders
- Plugins
- Mode
- Browser Compatibility

```javascript
// webpack의 config 파일 예시

module.exports = {
  target: ["web", "es5"],
  entry: "./src/script.js",
  output: {
    path: path.resolve(__dirname, "docs"),
    filename: "app.bundle.js",
    clean: true,
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, "css-loader"],
        exclude: /node_modules/,
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.resolve(__dirname, "src", "index.html"),
    }),
    new MiniCssExtractPlugin(),
  ],
  optimization: {
    minimizer: [new CssMinimizerPlugin()],
  },
};
```

## Target

Webpack은 다양한 환경과 target을 컴파일한다. target의 기본 값은 web이며, 적용하지 않으면 이 기본 값으로 적용된다. 이 부분에는 web 외에도 다양한 환경을 컴파일 할 수 있는데, esX를 넣으면 지정된 ECMAScript 버전으로 컴파일 할 수 있다.

```javascript
module.exports = {
  target: ["web", "es5"],
};
```

## Entry(엔트리)

webpack에서의 entry는 프론트엔드 개발자가 작성한 코드의 "시작점"으로 이해하면 편하다. React도 index.js에서 HTML 엘리먼트 하나에 React 코드를 적용하는 것 부터 시작한다.<br/>

Entry 속성은 Entry point라고도 하며, webpack이 내부의 디펜던시 그래프를 생성하기 위해 사용해야 하는 모듈이다. Webpack은 이 Entry point를 기반으로 직간접적으로 의존하는 다른 모듈과 라이브러리를 찾아낼 수 있다.

```javascript
// 기본 값
module.exports = {
  ...
  entry: "./src/index.js",
};

// 지정 값
module.exports = {
  ...
  entry: "./src/script.js",
};
```

기본 값은 **./src/index.js**이지만 webpack 설정에서 이런 식으로 Entry 속성을 설정하여 다른 (또는 여러) entry point를 지정할 수 있다.

## Output(출력)

Output 속성은 생성된 번들을 내보낼 위치와 이 파일의 이름을 지정하는 방법을 webpack에 알려주는 역할을 한다.

```javascript
const path = require('path');

module.exports = {
  ...
  output: {
    path: path.resolve(__dirname, "docs"), // 절대 경로로 설정ㅎ해야 한다.
    filename: "app.bundle.js",
    clean: true
  },
};
```

기본 출력 파일의 경우에는 **./dist.main.js**로, 생성된 기타 파일의 경우에는 **./dist** 폴더로 설정된다. 위의 예제에서는 `output.filename`과 `output.path` 속성을 사용하여 webpack에 번들의 이름과 내보낼 위치를 알려주고 있다. `path` 속성을 사용할 때는 path 모듈을 사용해야만 한다.

## Loader(로더)

Webpack은 기본적으로 JavaScript와 JSON 파일만 이해한다. 그러나 loader를 사용하면 Webpack이 다른 유형을 파일을 처리하거나, 그들을 유효한 모듈로 변환해 애플리케이션에 사용하거나 디펜던시 그래프에 추가할 수 있다.

```javascript
module.exports = {
  ...
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [MiniCssExtraPlugin.loader, "css-loader"],
        exclude: /node_modules/,
      },
    ],
  },
};
```

상위 수준에서 loader는 webpack 설정에 몇 가지 속성을 가진다.

- **`test`**: 변환이 필요한 파일들을 식별하기 위한 속성
- **`use`**: 변환을 수행하는 데 사용되는 로더를 가리키는 속성
- **`exclude`**: 바벨로 컴파일하지 않을 파일이나 폴더를 지정. (반대로 `include` 속성을 이용해 반드시 컴파일해야 할 파일이나 폴더 지정 가능)

여기서 `test`와 `use` 속성은 필수 속성이다. 이런 속성을 넣어 규칙을 정하기 위해서는 `module.rules` 아래에 정의해야 한다. 그저 `rules` 아래에 정의하면 webapck은 경고를 하게 된다.

## Plugins(플러그인)

Plugins를 사용하면 번들을 최적화하거나 에셋을 관리하고, 또는 환경변수 주입 등의 광범위한 작업을 수행할 수 있게 된다.

```javascript
const webpack = require('webpack');
const HtmlWebpackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
  ...
  plugins: [
    new HtmlWebpackPlugin({
      template: path.resolve(__dirname, "src", "index.html"),
    }),
    new MiniCssExtractPlugin(),
  ],
};
```

플러그인을 사용하기 위해서는 `require()`를 통해 플러그인을 먼저 요청해야 한다. 그리고 plugins 배열에 사용하고자 하는 플러그인을 추가해야 한다. 대부분의 플러그인은 사용자가 옵션을 통해 지정할 수 있다. 다른 목적으로 플러그인을 여러 번 사용하도록 설정할 수 있기 때문에 `new` 연산자를 사용해 호출하여 플러그인의 인스턴스를 만들어줘야 한다.<br/>

위의 예제에서 `html-webpack-plugin`은 생성된 모든 번들을 자동으로 삽입하여 애플리케이션용 HTML 파일을 생성해준다. `mini-css-extract-plugin`은 CSS를 별도의 파일로 추출해 CSS를 포함하는 JS 파일 당 CSS 파일을 작성해주게끔 지원한다.

## Optimiztion(최적화)

Webpack은 버전 4부터는 선택한 항목에 따라 최적화를 실행한다.

```javascript
module.exports = {
  ...
  optimization: {
    minizer: [
      new CssMinimizerPlugin(),
    ]
  }
};
```

최적화하기 위해 다양한 옵션이 지원되는데, 대표적으로 `minimize`와 `minimizer` 등을 사용한다.

- minimize: `TerserPlugin`또는 `optimization.minimize`에 명시된 plugins로 bundle 파일을 최소화(=압축)시키는 작업 여부를 결정
- minimizer: `default minimizer`를 커스텀된 `TerserPlugin` 인스턴스를 제공해서 재정의할 수 있다.

위의 예제에서는 `mini-css-extract-plugin`에 관련된 번들을 최소화하도록 지시하고 있다.
