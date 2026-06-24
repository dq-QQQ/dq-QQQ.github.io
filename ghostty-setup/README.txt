cmux/Ghostty 터미널 세팅 — 집 Mac에 적용하기
================================================

이 폴더에 든 것:
  - config              (ghostty 설정)
  - background.jpg      (배경 원본)
  - background-blur.jpg (배경 블러 사본, r2)

────────────────────────────────────────
방법 A) 이 저장소를 clone 해서 적용 (권장)
────────────────────────────────────────

  # 1) repo clone (이미 있으면 git pull)
  git clone https://github.com/dq-QQQ/dq-QQQ.github.io.git
  cd dq-QQQ.github.io/ghostty-setup

  # 2) D2Coding 폰트
  brew install --cask font-d2coding

  # 3) 설정 복사
  mkdir -p ~/.config/ghostty
  cp config background.jpg background-blur.jpg ~/.config/ghostty/

  # 4) 사용자명이 dq가 아니면 경로 자동 치환
  sed -i '' "s|/Users/dq/|$HOME/|g" ~/.config/ghostty/config

  # 5) 적용
  cmux reload-config      (또는 cmux에서 Cmd+Shift+, / 앱 재시작)

  검증: cmux config doctor

────────────────────────────────────────
방법 B) 파일만 직접 옮긴 경우 (zip/AirDrop 등)
────────────────────────────────────────

  위 2~5번과 동일. clone 대신 받은 폴더 안에서 실행하면 됩니다.

────────────────────────────────────────
참고
────────────────────────────────────────
- config 안의 background-image 경로는 절대경로(/Users/dq/...)예요.
  집 Mac 사용자명이 'dq'가 아니면 4번 sed 한 줄로 자동 치환됩니다.
- Catppuccin Mocha 테마는 ghostty 내장이라 별도 설치 불필요.
