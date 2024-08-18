# Axios
- 깃허브: https://github.com/axios/axios
- 예제에서는 https://reqres.in/ 를 사용했다.

# Axios 사용법

## 방법1: `index.html`에 CDN을 사용하는 방법
```html
<head>
    <script src="https://unpkg.com/axios@1.6.7/dist/axios.min.js"></script>
</head>
```

## 방법2: 패키지로 설치하는 방법
```bash
npm install axios
```

# GET 메소드
- 첫번째 parameter: 요청을 보낼 URL
- 두번째 parameter: 요청을 구성하는 config 객체 (Content-Type 등)

## 기본 방법
```js
function getData() {
    axios.get('https://reqres.in/api/users')
        .then(response => {
            console.log(response)
        })
}
```

## params를 포함하여 GET 메소드를 보내는 방법
- params: URL의 쿼리 문자열(Query String)에서 추출된 매개변수를 의미한다.

### params를 따로 두번째 parameter로 빼는 경우
```js
function getData() {
    axios.get('https://reqres.in/api/users', {
        params: {
            page: 8
        }
    })
        .then(response => {
            console.log(response)
        })
}
```

### params를 URL에 포함 시키는 경우
- `?` 다음부터 쿼리 문자열이다.
```js
function getData() {
    axios.get('https://reqres.in/api/users?page=3')
        .then(response => {
            console.log(response)
        })
}
```

### 이미지를 GET하는 방법

```js
import * as fs from 'fs';
import axios from "axios"

function createImage() {
    axios.get('https://picsum.photos/1000', {
        responseType: 'stream'
    }).then(res => {
        res.data.pipe(fs.createWriteStream('random-image.jpg'))
    })
}
```

- `responseType`은 HTTP 요청을 보내는 클라이언트가 응답을 받았을때, 자료를 어떤 형식으로 처리 할 지를 설정한다.

| ResponseType | 파일 형식      |
| ------------ | -------------- |
| stream       | 이미지         |
| blob         | 동영상, 오디오 |


- `pipe`는 응답 데이터를 어떻게 처리할지를 parameter로 받는다.


- 참고: https://github.com/axios/axios?tab=readme-ov-file#example

# POST 메소드
- 첫번째 parameter: 요청을 보낼 URL
- 두번째 parameter: 본문에 보낼 데이터
- 세번째 parameter: 요청을 구성하는 config 객체 (Content-Type 등)

```js
function sendData() {
    axios.post('https://reqres.in/api/users', {
        name: "최영우",
        job: "개발자",
    }).then(response => {
        console.log(response)
    })
}
```

# 에러 처리 방법
- axios는 `status`가 400이상인 경우 에러로 간주한다.

```js
function testErrorHandling() {
    axios.post('https://reqres.in/api/register', {
        email: "korea@naver"
    }).catch(error => {
        console.log(error)
    })
}
```

# 브라우저에 출력하는 방법

## Text를 받아서 브라우저에 출력하는 방법

### HTML 파일
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <script src="https://unpkg.com/axios@1.6.7/dist/axios.min.js"></script>
</head>

<body>
    <h1 id="random-quote"></h1>
    <script src="quoteGenerator.js" />
</body>

</html>
```

### JS 파일
```js
document.addEventListener("DOMContentLoaded", () => {
    let element = document.getElementById('random-quote')
    axios.get("https://api.quotable.io/random")
        .then(res => {
            let sentence = res.data.content
            element.innerText = sentence
        })
})
```

- `addEventListener`는 DOM element를 감시하는 기능을 한다.
- `DOMContentLoaded`는 HTML 파일이 모두 읽히고, DOM 트리가 완성이 됬을때를 의미한다.

## Image를 받아서 브라우저에 출력하는 방법

### HTML 파일
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <script src="https://unpkg.com/axios@1.6.7/dist/axios.min.js"></script>
</head>

<body>
    <img id="random-image"></img>
    <script src="imageGenerator.js" />
</body>

</html>
```

### JS 파일

```js
document.addEventListener("DOMContentLoaded", () => {
    let element = document.getElementById('random-image');
    axios.get("https://picsum.photos/500", {
        responseType: 'arraybuffer' // axios에서 이미지를 arraybuffer로 처리해 줘야 한다.
    })
        .then(res => {
            let imageString = base64ArrayGenerator(res.data);
            element.src = 'data:image/jpeg;base64,' + imageString; // 이미지 파일은 앞에 data:image를 붙여 줘야한다.
        })
        .catch(error => {
            console.error('Error fetching image:', error);
        });
});

/**
 * 1단계: input 버퍼를 8비트 배열로 만든다.
 * 2단계: 배열을 2진법 문자열로 만든다.
 * 3단계: 2진법 데이터를 Base64 문자열로 만든다.
 */
function base64ArrayGenerator(buffer) {
    let binaryData = ""
    // 1단계
    let array = new Uint8Array(buffer)
    for (let i = 0; i < array.byteLength; i++) {
        // 2단계
        binaryData += String.fromCharCode(array[i])
    }
    // 3단계
    let base64String = window.btoa(binaryData)
    return base64String
}
```