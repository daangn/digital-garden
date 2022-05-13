# Git

- [[Linus Torvalds]]가 개발한(계속 하고 있음) 분산 [[VCS]]

- [[GNU GPL v2 (License)]]로 라이센싱 된 [[오픈소스]] 프로젝트
  - [https://github.com/git/git/blob/master/COPYING]

- 대소문자 이슈
  - git에서 대소문자를 무시해서, 대소문자 변경시 버전관리에 버그가 발생함 (기존 파일이 변경되지 않는 이슈)
  - 해결방법
    1. `git mv OldFileName NewFileName` (git으로 파일명 변경)
    2. `git config core.ignorecase false` (git config 변경)
    3. `git rm -r --cached` (캐시 이슈 발생시 캐시 삭제)
