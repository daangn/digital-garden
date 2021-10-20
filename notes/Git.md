# Git

- 버전관리도구

- 대소문자 이슈
  - git에서 대소문자를 무시해서, 대소문자 변경시 버전관리에 버그가 발생함 (기존 파일이 변경되지 않는 이슈)
  - 해결방법
    1. git mv OldFileName NewFileName (git으로 파일명 변경)
    2. git config core.ignorecase false (git config 변경)
    3. git rm -r --cached (캐시 이슈 발생시 캐시 삭제)