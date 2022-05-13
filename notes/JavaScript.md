# JavaScript

- [[프로그래밍 언어]]

- 웹 브라우저에서 실행되는 유일한 범용 프로그래밍 언어

- [[ECMA International]] 표준으로 등재되어 있다.
  - [ECMA-262: ECMAScript® (연도) language specification](https://www.ecma-international.org/publications-and-standards/standards/ecma-262/)
  - ECMA에 등재된 표준화된 스크립트 언어로, 공식적인 명칭은 **ECMAScript**이다.
  - 공식 기술 위원회인 **TC39**에 의해 매년 스펙이 개정된다.

- [ECMAScript와 TC39](https://ahnheejong.name/articles/ecmascript-tc39/)
  - ECMAScript 언어 표준과 TC39
    - 자바스크립트는 ECMA-262을 만족하는 구현체를 가리킨다. Ecma 인터내셔널의 여러 기술 위원회(Technial Committee, 이하 TC) 중 **TC39 라는 위원회가 이 명세를 관리한다**.
  - ECMAScript 언어 표준
    - 1997년 6월에 발표된 첫 번째 판(edition)을 시작으로 2017년 12월 현재까지 ECMA-262의 총 8개 판이 존재한다. 각 판은 판 번호 또는 발표된 연도를 따라 이름붙여진다. 예를 들어, 2015년에 발표된 6판의 경우 ECMAScript2015 또는 ECMAScript6 이라 (또는 ECMAScript를 ES로 줄여 ES2015 또는 ES6이라) 불리운다.
  - Technical Committee 39
    - Ecma 인터내셔널의 여러 기술 위원회(Technial Committee, 이하 TC) 중 ECMA-262 명세의 관리는 TC39 위원회가 맡고 있다.. TC39의 구성원 목록은 Mozilla, Google, Apple, Microsoft 등의 메이저 브라우저 벤더를 비롯해 Facebook, Twitter 등의 다양한 단체로 이루어져 있다. 대부분의 구성원이 표준을 올바르게 구현해야 할 책임을 갖는, 언어 표준의 변화에 직접적으로 영향을 받는 단체다. 엄밀히는 기업/단체가 구성원이지만, 'TC39 구성원' 이라는 용어가 해당 기업/단체가 보낸 대리인을 지칭하는 경우도 많다.
    - TC39는 정기적으로 만나 회의를 진행하는데, 회의록은 모두 [웹상에 공개된다](https://github.com/tc39/tc39-notes). **TC39에서 내리는 결정이 단순 다수결이 아닌 컨센서스 체제로 이루어진다는 점은 주목할 만 하다**
  - TC39 프로세스
    - ECMA-262 표준에 새로운 명세를 추가하기 위한 과정은 공식적으로 명문화되어 있다. [TC39 프로세스](https://tc39.github.io/process-document/)라고도 불리는 이 과정은 0단계부터 4단계까지 총 5개의 단계로 나누어져 있으며, **각 단계로의 승급을 위한 명시적인 조건들이 존재한다**. 해당 조건을 만족한 이후 위원회의 동의를 얻은 프로포절만이 다음 단계로 넘어간다. 물론 그 과정에서 최종적으로 표준에 편입되지 않기로 결정되어 버려지는 제안들도 존재한다.
    - 모든 프로포절은 [TC39의 깃헙 단체 계정](https://github.com/tc39)의 [proposals 저장소](https://github.com/tc39/proposals)에 등재된다. 2017.12.19 기준, 0단계의 경우 `stage-0-proposals.md` 파일에서, 4단계에 이르러 표준에 편입된 프로포절은 `finished-proposals.md` 파일에서 확인할 수 있다. 활성화된 프로포절(active proposal)이라 불리는 1-3단계 프로포절의 경우 README.md에 등재되어 있다. 대부분의 프로포절은 별도의 저장소를 갖고 있고, 그 곳에선 해당 프로포절을 어떻게 발전시킬지, 어떤 어려움이 예상되는지 등의 다양한 논의가 이루어진다.
