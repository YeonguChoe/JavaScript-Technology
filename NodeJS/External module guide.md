# 상황에 따른 외부 모듈 사용 방법

## Vanilla JS와 브라우저를 사용하는 경우
- CDN을 사용해야 한다.
- `index.html`의 헤더에 CDN을 추가한다.

```html
 <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
```

## React/Angular와 브라우저를 사용하는 경우
- `ts/js` 파일에서 `import`문 또는 `require`문을 사용한다.
```js
import axios from 'axios';
```
또는
```js
const axios = require('axios');
```

## NodeJS를 사용하는 경우
- NodeJS를 사용할 때는 CDN을 사용하지 않는다.
- `package.json`에서 `type`으로 모듈 시스템을 변경 할 수 있다.
 
| 모듈시스템 | 출시일 | 외부모듈 사용방법                      |
| ---------- | ------ | -------------------------------------- |
| CommonJS   | 2009   | const module = require('module_name'); |
| ES6        | 2015   | import { 변수, 함수 } from 'js파일';   |

## 브라우저를 사용하는 경우
- 브라우저의 콘솔을 사용하는 경우 외부 모듈을 import할 수 없다.