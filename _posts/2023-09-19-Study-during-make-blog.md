---
title: "Jekyll로 블로그를 만들긴 했는데, Jekyll이 뭐야?"
date: 2023-09-19 22:21:00 +09:00
categories: [Dev, Web]
# tags: [writing]
render_with_liquid: false
---

최근에 깃허브 블로그를 무작정 🤛**구글링 파워**🤜로 만들었고, 가장 쉽게 접할 수 있었던 Jekyll이란 테마를 이용했다. 이걸 한 선배에게 얘기하게 되었고, **"jekyll로 만들었어? gatsby로 같이 만들어볼래?"** 라는 제안을 받게 되었다.

gatsby는 뭐고.. 내가 여태 빌드하면서 사용했던 명령어(ruby).. 하며, 빌드한 결과물로 만들어졌던 gem파일 하며.. 이러한 모든 것을 이해하면서 사용한 것이 아니라 단순히 따라하기에 급급했기에 만들며 사용했던 jekyll에 대해 속속이 공부해보려고 한다.


|    |    |
|-------|-------|
| ![](/assets/img/zzal/chiikawa.jpg) | ＿人人人人人人人＿<br>＞ 공부 같이하자！＜<br>￣^Y^Y^Y^Y^Y^￣<br> |

## 개념 익히기
### Jekyll이란?
- **정적 사이트 생성기** : 동적인 웹 애플리케이션과는 달리 정적인 웹 사이트를 생성하는 도구. 웹 사이트의 콘텐츠를 사전에 생성하여 HTML파일로 만든다. 
  내가 만든 블로그는 이 정적 파일을 웹 서버에(github를 통해) 호스팅하기만 한 것!
- Jekyll의 특징 : **Ruby로** 작성됨. Markdown으로 콘텐츠를 작성하고, **Liquid 템플릿 엔진**을 사용해 빠르게 웹 사이트를 생성한다.

### Ruby란?
- **동적 프로그래밍 언어** : 프로그램이 실행될 때 데이터 타입을 미리 지정하지 않고, 런타임에 변수의 타입이 동적으로 결정되는 프로그래밍 언어. (동적 타이핑이라고도 함.)
- 객체지향 프로그래밍 언어의 일종.
- 가비지 컬렉션을 통해 메모리 관리를 자동으로 처리함.
- 인터프리터 언어(스크립트 언어)로, 코드를 수정 후 즉시 실행이 가능

### Gem이란?
- Ruby 프로그래밍 언어에서 사용되는 패키지 관리 도구.
- Ruby 프로젝트에서 사용되는 라이브러리와 의존성 패키지를 설치할 수 있다.

### Liquid 템플릿 엔진이란?
- 웹 애플리케이션과 웹 사이트에서 동적인 콘텐츠를 생성하는 데 사용되는 템플릿 엔진 중 하나이다.
- 간단하고 직관적인 문법으로 이루어져있다.
- 변수의 값을 HTML 문서에 출력이 가능.
- 모듈화된 디자인을 구현하기에 용이하다.

## Jekyll 블로그 만들며 사용한 명령어/파일 분석하기
1. `npm install`
   - npm(Node Package Manager)을 이용해 Node.js 프로젝트에서 사용하는 패키지(라이브러리)를 설치하는 명령어. 모듈을 설치하는 것.
   - 다음과 같은 과정을 거친다. **의존성 확인**(`package.json` 파일에서 정의된 종속성(dependencies) 목록을 확인), **패키지 다운로드**, **로컬 설치**(다운로드 한 패키지를 프로젝트의 `node_modules`디렉토리에 설치함.)
2. `npm run build`
   - 프로젝트를 빌드하고, 하나의 파일로 번들링하거나 압축하여 성능을 최적화 하고, 빌드 환경에 맞게 설정을 다르게 조정하고, 에러를 확인하고 테스트하기도 한다.
   - package.json 파일에 정의된 스크립트 중 하나를 실행하는 것이다.
3. `jekyll serve`
   - 로컬 개발 서버가 시작되어 Jekyll 프로젝트를 로컬에서 실행할 수 있다.
   - 소스 코드 수정 시 변경 사항을 감지하여 자동으로 리로딩한다.
   - 만약 Jekyll이 설치되어있지 않다면 `gem insatll jekyll` 명령어를 통해 설치할 수 있다.
4. 💾 `jekyll.yml`
   - Jekyll의 설정 파일.
   - 프로젝트의 루트 디렉토리에 위치해있다.
   - YAML(YAML Aint Markup Language)형식으로 이루어짐.
   - 사이트, 테마, 플러그인, 데이터 디렉토리, 포스트 기본 경로 등에 대해 설정할 수 있다.


다음 포스팅에서는 선배가 제안했던 **gatsby에** 대해 알아보고자 한다.


---
<!--
### 서버에 대하여 간단히 이해하기
우리가 프로그램을 만들 때 인터넷을 이용해서 다른 곳의 데이터를 가져와 보여주거나, 다른 곳에서 보내온 데이터를 우리 컴퓨터에 저장하는 경우가 많이들 있다. 이렇게 다른 곳에 있는 단말에 데이터를 달라고 요청하는 프로그램을 **클라이언트**, 다른 고셍서 요청받은 명령을 처리해주는 프로그램을 **서버**라고 한다.

우리가 만든 프로그램을 인터넷에 연결하기 위해서는 단말기에 네트워크 카드가 달려있어야 한다. 두 개의 서로 다른 단말기에 모두 네트워크 카드가 들어 있다면 한쪽은 클라이언트, 다른 한 쪽은 서버 역할을 할 수 있다. 이 때 서버는 포트를 지정하여 그 포트로 요청을 받을 수 있다. 하나의 단말에서 사용할 수 있는 포트는 보통 0~65535중 하나를 지정해서 사용하고, 보통 아래와 같이 포트의 범위가 구분된다.
| 포트 번호   | 설명   |
|-------|-------|
| 0~1023 | 잘 알려진 포트 |
| 1024~49151 | 등록된 포트 |
| 49152~65535 | 동적 포트 |

윈도우나 안드로이드 같은 OS가 시작될 때는 이미 잘 알려진 포트에서 대부분을 사용한다. 따라서 우리가 직접 만드는 서버 프로그램은 보통 1024번 이상의 포트 번호를 사용한다.

서버를 만들어 실행하면 클라이언트로부터 요청을 받아 처리하게된다. 또한 많은 경우에, 서버는 데이터베이스에 연결할 수 있도록 구성되기 때문에 클라이언트에서 보내온 데이터를 저장하거나 저장된 데이터를 조회한 후 클라이언트에 보내준다. 서버 중에서 우리가 많이 사용하는 웹 브라우저에서 접속하는 서버를 **웹 서버**라고 하고, HTTP 프로토콜을 사용한다.

<details>
<summary>프로토콜이란</summary>
    데이터를 서로 어떤 형태로 주고받을 지 정한 것. 간단하게 말하면 데이터의 형태.
</details>
-->