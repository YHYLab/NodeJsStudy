<p align="center">
    <img src="resource/img/Nodejs_logo.png" width="200px">
</p>

# Study NodeJS :octocat:

## NodeJS란?
NodeJS는 하나의 독립된 javascript의 실행환경을 제공해주는 플랫폼이다.
NodeJS 이벤트 기반이고 비동기기반이다.
메인스레드에 블록킹이 발생하지 않기 때문에 대용량 서비스에도 적합하다.

## 이벤트 기반
<p align="left">
    <img src="resource/img/EventLoop.jpg" >
</p>
Node.js 는 싱글스레드 프로그램이고 이벤트와 콜백을 이용하기 때문에 높은 성능을 제공한다. 

Node.js 의 이벤트 기반은 옵저버 패턴으로 작동된다. 프론트 엔드 단의 옵저버 패턴과 완전히 같다. 

Node.js 싱글스레드는 while(true) 와 같은 이벤트 loop를 실행한다. 

## 장점 & 단점
장점 | 단점
----- | -----
이벤트 기반이고 대규모 시스템에 적합하다 | 단일 스레드 방식이여서 한곳에서 문제가 발생하면 전체 시스템에 영향준다.
Javascript는 대부분  개발자에 익숙한 언어여서 접근성이 좋다. | JS는 버그도 있다.
Gogoole이 c++로 개발한 V8 JS엔진을 사용한다 | 속도는 c/c++로 개발한것보다 빠르지는 않다.
많은 오픈된 NPM 모듈을 사용할 수 있다. | NPM 모듈에 악의성 코드가 숨어있을 수 있다.

### 현존하는 JS엔진
단체 | 엔진 
----- | -----
Internet Exploer | Chackra
Google | V8
Mozila | Spider Monkey
Apple | Squirrel Fish
Opera | Karakan 

## 설치
[http://nodejs.org](http://nodejs.org)
Windows, Linux, MacOS를 지원한다.

## 프롬프트 실행 모드

```javascript
>node
>colsole.log('Hello, World!');
Hello, World!
```
## JS 파일 실행 

helloWorld.js
```javascript
console.log('Hello, world!');
```

```javascript
>node helloWorld
Hello, world!
```

## NodeJS의 전역객체
객체 | 설명
----- | -----
console | console프린트 기능
exports | 모듈관련 기능
process | 프로세스 객체 
time | setTimeout, setImmediate, setInterval, clearTimeout, clearImmediate, clearInterval


### console 객체
메서드 | 설명
----- | -----
log |
info |
warn |
error |
dir |
time |
timeEnd |
trace |
assert |
Console |

### process 객체
속성 | 설명
----- | -----
argv | 파라미터
env | 실행환경
version | NodeJS버전
versions | NodeJS버전과 의존성 모듈의 버전
arch | 운영체제의 아키틱처
platform | nodejs플랫폼

process객체에는 stdout，stdin,stderr기본 입출력 메서드와 kill, exit등 메서드가 있다.
process는 EventEmitter구현이다.

process.exit() 실행하면, process.on('exit', function(err) {
    console.log(err);
})로 exit 이벤트를 재구현 할 수 있다.

process.on('uncaughtException',()=>{}) 는 에러발생시 좋은  방법일까?
더 좋은 방법은?

### exports 객체
exports는 재사용할 객체를 정의하고, require메서드는 함수를 불러온다.  
module.js
```javascript
    exports.add = (a, b) => {
        return a + b;
    };

    exports.mod = (a, b) => {
        return a % b;
    };
```

main.js
```javascript
    var module = require('./module.js');

    var sum = module.add(1, 3);
    console.log(sum);

    var mod = module.mod(7, 2);
    console.log(mod);
```

## 기본 내부 모듈
모듈명 | 기능
----- | -----
os | 운영체제 정보
url | url문자열과 url객체 상호전환. url문자열의 조립 등 기능
query strings | url문자열과 url객체 상호전환，url에 이미 존재하는 기능이여서 많이 사용되지 않는다
util | 각종 util
crypto | Hashing, 암호화/복호화 기능
fs | 파일 입출력
http[s] | http[s]서비스에 관련된 모듈

path, tls/ssl, cluster, debugger, dns등 모듈도 있다.
모듈의 상세 api : [https://nodejs.org/dist/latest-v8.x/docs/api/](https://nodejs.org/dist/latest-v8.x/docs/api/)
## 외부 모듈
외부 모듈을 사용할 때에는 npm을 이용해 설치 해야 한다. 
```javascript 
    >npm install -g XXX
```
-g 옵션은 전역 모듈지정.
--save 옵션은 설치한 버전정보등을 package.json에 관리. 

프론트 관련 모듈에는 ejs,jade
에러발생시 서버 자동 재시작에는 supervisor, foreve
express는 더 많은 http기능을 제공한다.  
socket.io패키지는 socket에 관련 기능을 제공한다.
유닛테스트 관련 모듈에는 Mocha, Jasmine, Jest등이 있다.
# 면접문제
## libuv은 무엇인가？
libuv는 강제로 비동기를 사용하게 하는 이벤트기반의 프로그램 방식이다. 핵심 기능은 하나의 event-loop를 제공하고 I/O기반과 기타 이벤트 알림의 콜백함수를 제공한다. libuv는 핵심 툴도 제공한다. 알람, 난블록킹 네트워크의 지원, 비동기 파일의 접근, 자식 프로세스 등이다.
