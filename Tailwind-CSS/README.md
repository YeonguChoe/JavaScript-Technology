# Tailwind CSS

## [React에서 설치 방법](https://tailwindcss.com/docs/guides/create-react-app)

1. Tailwind CSS가 프로덕션 코드에는 CSS 코드를 생성하기 때문에 development dependency로 추가한다.
```bash
npm install --save-dev tailwindcss
```

2. `tailwind.config.js`를 생성한다.
```bash
npx tailwindcss init
```

3. `content`에 Tailwind CSS가 사용되는 모든 코드들을 추가한다.
```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./src/**/*.{js,jsx,ts,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

4. `index.css`파일에 Tailwind CSS 지시어를 추가한다.
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

- `@tailwind base;`: 브라우저에서 사용되는 기본 스타일을 추가한다.
- `@tailwind components;`: 버튼이나 카드와 같은 컴포넌트의 스타일을 추가한다.
- `@tailwind utilities;`: padding, margin, color 처럼 개별 태그에 스타일을 추가한다.
