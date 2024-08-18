# 노드JS 설치 방법
- 패키지 매니저나 인스톨러 보다, Prebuilt Binary를 다운로드 받아서 경로를 추가하는 방법이 가장 확실하다.
- 다운로드 받은 폴더 `node-v22.3.0-darwin-arm64`는 `/usr/local/` 안에 저장한다.
- `.zshrc` 파일에 `export PATH=/usr/local/node-v22.3.0-darwin-arm64/bin:$PATH`를 추가한다.