![CI](https://github.com/jaeyeoljo/app/workflows/CI/badge.svg)

# Notion 핵심 기능 clone 코딩

TypeScript를 사용하여 OOP기반 아키텍쳐 설계

1. TypeScript, CSS, HTML를 사용하여 구현
2. Notion 등록 및 드래그 기능 구현

# TypeScript + OOP(Object-Oriented Programming)

React 라이브러리 도움없이 컴포넌트를 만들어 React의 기본기능 구현

1. TypeScript
2. CSS
3. HTML
4. Webpack3
5. Webpack-Dev-Server
6.
7.
8.
9.

# 어떤 사람들에게 필요한 프로젝트인가요?

보통 을 통하여 구현한 프로젝트의 백엔드 소스코드를 제공하기 위해 만들었습니다.

## 부여된 조건

1. 등록 기능 구현 (이미지 / 영상 / 글 / 스케쥴 등록이 가능해야한다)
2. 드래그 기능 구현 (각 섹션별로 드래그해서 끼워넣기가 가능해야한다)
3. ㅇㅇㅇㅇ 기능 구현
4. 디버깅은 Chrome Debugging을 사용을 위해 sourceMap을 설정한다
5. ㅇㅇㅇㅇ

상기 내용을 모두 충족하면서, 결과적으로 디플로이 환경은 ㅇㅇㅇ이 되고, ㅇㅇㅇ 기반 애플리케이션이 실행되는 환경을 만드는데 초첨을 두었습니다.

# 사용해보기

## 1) 파이썬3 패키지 설치

```bash
pip install -r requirements.txt
```

## 2) 노드 패키지 설치

```bash
cd static/myapp
npm install 또는 yarn install
```

## 3) 백엔드 서버 기동 (python app.py 백그라운드로 실행) : loaclhost:5000

```bash
python app.py test > /dev/null 2>&1 &
```

> 해당 백엔드 서버는 나중에 디플로이할때의 환경이 되며, 프런트서버에서 api호출할 경우, 해당 서버를 바라보게 됩니다.
> 즉, 프런트 개발서버를 기동전에 해당 app.py을 실행시켜두어야 합니다.
> 이 상태에서 5000번에 접속해보면 아무것도 뜨지 않을텐데요 이유는 Flask가 static/dist 폴더를 기본으로 바라보고있기 때문입니다. 5)번에서 처럼 yarn build를 하고나면 Front의 View가 반영되겠죠?

## 4) 프런트엔드 개발서버 기동 (Webpack Dev Server) : localhost:8080

```bash
yarn start
```

> Webpack-dev-server를 이용한 프런트용(HMR) 개발서버가 기동이 됩니다.

## 5) 디플로이 하기

```bash
yarn build
```

> 해당 webpack.config.js를 보면, webpack-dev-server의 설정에서 라우트 패스가 /api일 경우 proxy: localhost:5000을 보게 되는 원리로 되어있습니다.
> 따라서 프런트에서 /api 패스에 접속시 React-router가 아닌 Flask.app route를 타게됩니다.
> 추가적으로 yarn build를 하는 순간, 백엔드 서버는 빌드된 static/dist의 소스들을 바라보게 되고 프런트와 같은 환경이 되게 됩니다.

# 번들링 (Webpack3)

-   현재 웹팩 config을 보면 아시겠지만, SPA(Single Page Application)로 구성되어있습니다. React-router로 DOM을 새로 그리는 방법을 채택했습니다.
    > static/resource 에서 외부 부트스트랩이나 딱히 번들링할 필요없는 소스들을 모아둘 수 있습니다. (index.html에 상대경로로 연결)
    > 작업을 하시다보면 번들링 되는 속도나 번들링시 발생하는 예기치않은 오류를 무시하고 그냥 소스만 연결해야 할 상황(부트스트랩에 이미지가 빠져있다던가)이 분명히 있을거에요.
    > 두 언어가 같은 경로에 놓여지도록 python서버와 webpack-dev-server의 public path를 맞춰논 상태입니다. 소스 연결시에는 jinja2({{url_for()}})를 이용하거나 혹은 상대경로를 이용할 수 있을텐데, 저는 그냥 상대경로로 설정하는게 편했습니다.

# 디버깅 로그

1. 웹팩 빌드시 entry를 변경했으나, 변경점이 번들링 되는 html에 반영이 되지않음(2018/01/30)
    > 해결볍) jinja2 템플릿 언어 테스트를 위해 webpack.config.js의 proxy에 '/'인덱스를 넣어둔것이 문제였음. 백단 서버가 기동되고 지속적으로 물고있었기에 변경점이 반영이 안됨. 따라서 '/'를 빼고 정확히 jinja2 템플릿 언어를 사용해야 하는곳에 프록시를 넣어주어함.

# 디플로이

-   혹시 디플로이 환경이 AWS lambda이거나 엔드포인트가 존재하나요?
-   webpack의 output > publicPath를 설정해주세요.
-   flask의 static_url 을 설정해주세요.
    > ex) 디플로이 path가 hidekuma.com/dev 일 경우, 상기 처럼 publicPath와 static_url을 /dev로 설정해주어야 합니다.

# 라이센스

-   배포 및 수정이 가능합니다.
    > 본 소스코드는 학습에 한하여 자유롭게 수정 및 배포가 가능합니다. 누구나 필요에 따라 수정 및 재사용하실 수 있으며 기능과 오류등을 개선하기 위한 PR(Pull-Request) 요청으로 참여가 가능합니다.
    > 또한 문의사항이 있을 경우 devscripter@gmail.com으로 연락주십시요. 여러가지 이유로 이제부터 JavaScript는 TypeScript 없이는 현업에서 사용할 수 없는 언어가 될 것입니다.
