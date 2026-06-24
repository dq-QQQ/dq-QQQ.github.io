cmux/Ghostty 터미널 세팅 — 집 Mac에 적용하기
================================================

이 zip 안에 든 것:
  - config              (ghostty 설정)
  - background.jpg      (배경 원본)
  - background-blur.jpg (배경 블러 사본, r2)

────────────────────────────────────────
적용 순서
────────────────────────────────────────

1) D2Coding 폰트 설치 (집 Mac에 없으면)
     brew install --cask font-d2coding

2) 설정 폴더에 파일 복사
     mkdir -p ~/.config/ghostty
     cp config background.jpg background-blur.jpg ~/.config/ghostty/

   ※ config 안의 background-image 경로는 절대경로(/Users/dq/...)예요.
     집 Mac의 사용자명이 'dq'가 아니면 config의 두 경로를
     실제 홈 경로로 바꿔야 합니다. (아래 한 줄로 자동 치환 가능)

     sed -i '' "s|/Users/dq/|$HOME/|g" ~/.config/ghostty/config

3) 적용
     cmux reload-config      (또는 cmux에서 Cmd+Shift+, / 앱 재시작)

   검증: cmux config doctor

────────────────────────────────────────
참고: Catppuccin Mocha 테마는 ghostty 내장이라 별도 설치 불필요.
