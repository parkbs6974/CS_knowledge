<h1>Event-Driven Architecture (EDA)</h1>

## Event-Driven Architecture 요약

```
이벤트 기반 아키텍처는 특정 **사건(이벤트)**이 발생했을 때 미리 정의된 작업을 수행하는 아키텍처 패턴입니다.
```

EX) 누군가 문을 두드리는 소리(이벤트)를 듣고 문을 여는 것같이,시스템 내부에서 발생하는 다양한 사건에 반응하여 동작 한다.

## Event-Driven Architecture 주요 개념:

- Event (이벤트) : 상태 변화나 동작을 알리는 메시지입니다.
  ex) 사용자가 버튼을 클릭하거나 파일이 업로드되는 것 등이 이벤트이다.

- Event Emitter (이벤트 발생자) : 이벤트를 생성하거나 발생시키는 주체입니다.

* 이벤트 발생 : 이벤트가 발생하면 시스템은 이를 감지하고 관련된 처리 로직을 실핸 한다.

- Event Listener (이벤트 리스너) : 발생된 이벤트를 듣고 그에 반응하는 주체입니다.

- Handle (핸들러), callback : 특정 이벤트가 발생했을 때 실행되는 함수나 로직입니다.

## Node.js와 Event-Driven Architecture

- Node.js는 기본적으로 Event-Driven Architecture를 기반으로 설계되어있다.

- Node.js는 비동기, 논블로킹 I/O 작업에 의존하며, 이벤트와 콜백을 활용하여 동시성을 처리하고 있다. => <B>참고 페이지</B>

* Node.js는 싱글 스레드에서 동작하기 때문에 이벤트 기반 모델을 통해 웹 서버, 파일 시스템, API 같은 I/O 중심 작업에서 매우 효율적으로 작동합니다.

### Node.js에서 Event-Driven Architecture 적용 방식:

1. 이벤트 발생자(Event Emitter): Node.js에는 내장된 EventEmitter 클래스가 있습니다. 이 클래스는 이벤트를 발생시키고, 이벤트가 발생했을 때 등록된 리스너들을 호출합니다. EventEmitter는 이벤트 기반 아키텍처의 핵심 요소입니다.

```js
const EventEmitter = require("events");
const eventEmitter = new EventEmitter();

// 이벤트 리스너 등록
eventEmitter.on("sayHello", () => {
  console.log("Hello World!");
});

// 이벤트 발생
eventEmitter.emit("sayHello");
```

2.비동기 작업 처리: Node.js는 이벤트 루프를 사용해 비동기 작업을 처리합니다. 예를 들어, 파일 읽기 작업이 완료되면 on 메서드로 등록된 콜백 함수가 실행됩니다.

```js
const fs = require("fs");

fs.readFile("example.txt", (err, data) => {
  if (err) throw err;
  console.log("File read completed!");
});

console.log("File reading started!");
```

위 코드에서 readFile 함수는 비동기적으로 파일을 읽고, 파일이 읽히면 콜백이 실행되어 "File read completed!"를 출력합니다. 이 작업이 완료되기 전에 "File reading started!"가 먼저 출력됩니다. 이는 Node.js가 비동기 처리와 이벤트 기반 모델을 통해 블로킹 없이 효율적으로 작업을 처리하는 방식입니다.

### 요약:

Node.js의 Event-Driven Architecture는 이벤트를 발생시키고, 그에 반응하는 방식으로 작동하여 비동기 I/O 작업에서 매우 효율적입니다. 이 덕분에 Node.js는 많은 연결을 동시에 처리해야 하는 웹 서버나 API 서버 구축에 매우 적합합니다.

### Reference :

- AWS 이벤트 기반 아키텍처: https://aws.amazon.com/ko/what-is/eda/
- Red Hat 이벤트 기반 아키텍처: https://www.redhat.com/ko/topics/integration/what-is-event-driven-architecture
