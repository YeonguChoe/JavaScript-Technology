# JavaScript

## Node.js 런타임
- [설치 방법](NodeJS/Installation%20guide.md)
- [외부 모듈 사용 방법](NodeJS/External%20module%20guide.md)
- [Node-API를 이용해서 C/C++ 코드를 사용하는 방법](https://nodejs.org/api/n-api.html)

## Tool
- [Webpack]()
- React
- React-Router
- [Tailwind CSS](Tailwind%20CSS)

### REST API
- Fetch API
- ~~[Axios](Axios)~~

### WebSocket
- [WebSocket](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket)

## NPM

- npx가 안될때 .npm 디렉토리이하의 모든 파일들에 rwx 권한을 부여한다.
    - `chmod`는 change mode (권한)의 줄임말이다.
    - `-R`은 재귀적으로 디렉토리 이하에 chmod를 실행한다는 것을 의미한다.
    - `777`은 읽기 4, 쓰기 2, 실행 1의 합이라서 7이다.

```bash
sudo chmod -R 777 /Users/yeonguchoe/.npm
```
