# Babel

- 문서: https://babeljs.io/docs/babel-cli/

## 패키지 다운로드

```bash
npm install --save-dev @babel/core @babel/cli
```

## 사용법

### 파일 변환 방법
```bash
npx babel index.js --out-file output.js
```

### 폴더 변환 방법
```bash
npx babel src_dir --out-dir out_dir
```

## Babel 스크립트 작성 방법
- 파일 이름: `babel.config.json`

```json
{
  "presets": [
    [
      "@babel/preset-env",
      {
        "targets": {
          "edge": "17",
          "firefox": "60",
          "chrome": "67",
          "safari": "11.1"
        }
      }
    ]
  ]
}
```