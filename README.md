## 1-1) 사전과제 진행 가이드

- 아래 총 5 문제에 대한 해설을 작성한 뒤 Pull Request를 날려주세요.
- 문제 해설에 대한 정해진 양식은 없으며, 최대한 자세히 해설해주시면 좋습니다.
- 문제 유형은 해당 코스에서 다룰 주제들을 포함하고 있으니 완벽히 이해하시면 코스를 수강하는데 큰 도움이 될 것입니다.

**문의 사항은 사전 과제 Repository의 Issue로 등록해 주세요.*
  


## 1-2) 사전 과제

- (1) 동기와 비동기 프로그래밍에 대한 차이점을 설명해주세요.

동기는 작업을 순서대로 처리하는 방법으로 진행 중인 작업을 처리하다가 다른 작업을 요청하면 진행 중인 작업을 중단하고 요청한 작업의 응답이 올 때까지 계속 기다리면서 작업을 하나씩 처리해가는 방식이다. 순차적으로 처리하기 때문에 복잡하지 않고 문제가 발생하는 일이 적지만 한 작업을 완전히 처리한 뒤 다음 작업을 처리하기 때문에 응답이 오래 걸리는 작업이 있으면 아무것도 하지 못하고 기다려야 한다는 단점이 있다.

비동기는 작업을 병렬적으로 처리한다. 작업을 처리하다가 다른 작업을 요청한 후에 응답을 기다리지 않고 원래 하던 작업이나 요청한 작업을 제외한 또 다른 작업을 제외한 또 다른 작업을 처리한다. 요청한 작업은 콜백 방식으로 응답이 오게 되고 현재 진행 중인 작업이 없을 때 처리한다. 앞서 말한 동기방식의 단점을 비동기 방식을 이용하면 응답을 기다리는 동안 다른 작업을 처리할 수 있어서 전체적인 작업 속도를 단축할 수 있다. 하지만 작업을 순서대로 처리하는 과정이 필요하다면 비동기 방식은 적절하지 않다.

동기와 비동기는 코드를 이용해 작업을 처리하는 모든 곳에서 사용된다. 스레드와 스레드, 클라이언트와 서버 등 데이터를 주고받는 작업을 처리하는 모든 곳에서 동기와 비동기 방식이 사용된다. 

- (2) 블로킹과 논블로킹의 차이점을 설명해주세요.

동기와 비동기에 있는 특성으로 블록은 '막는다'는 의미로 현재 진행 중인 작업에서 다른 작업을 요청하면 응답에 대한 '완료'가 될 때까지 아무것도 할 수 없게 만드는 것이다. 논블록은 요청한 응답이 완료될 때까지 기다리지 않는다. 동기 방식에서는 사용하는 의미가 없지만 비동기에서의 논블록은 여러 개의 작업을 처리하게 해준다.

동기+블록은 A에서 B로 작업을 요청하고 응답을 기다림과 동시에 작업도 중단하는 것이다. 동기+논블록은 A에서 작업 B를 실행했을때 동기이므로 응답을 기다리지만 논블록이기 때문에 작업이 완료될 때까지 기다릴 필요가 없다. 그래서 진행 중이던 작업 A를 계속 하려고 하지만 동기 상태이기 때문에 응답이 올 때까지 기다려야 하므로 작업하지 못하는 상황이 된다. 이처럼 동기+논블록은 작업을 할 수 없게 충돌이 발생하므로 실제로는 거의 사용하지 않는다.

비동기+블록은 A에서 B로 요청할 때 블록을 하면 작업 A를 중단하는 것이다. 즉 A는 작업을 기다리진 않지만 B가 완료될 때까지 중단해야 하므로 A, B가 아닌 C, D작업 등을 할 수 있게 된다. 하지만 동기+논블록과 같이 거의 사용되지 않는다. 비동기+논블록에서는 A에서 B에서 요청을 했을 때 A가 작업의 권한이 있고 B의 응답도 기다리지 않기 때문에 원하는 일을 자유롭게 할 수 있다. 요청한 작업 B를 제외하한 작업 A, C, D 등 여러 다른 작업을 할 수 있어 매우 효율적이다. 비동기+논블록은 두 가지 일이 독립적일 때 사용한다.

- (3) 본인이 주로 사용하는 언어에서 비동기 프로그래밍을 사용하는 방법을 설명해주세요.
[Java, Spring]

쓰레드를 이용하여 비동기 프로그래밍을 한다. 쓰레드는 프로세스보다 더 작은 작업 단위로 경량 프로세스라고도 칭한다. 프로세스는 실행부터 종료까지 최소한 1개 이상의 쓰레드를 가지고 있다. JAVA는 Multi-thread Programming을 지원한다. 여러 작업 요청이 들어오면 여러개의 쓰레드에서 비동기적으로 작업을 처리한다.
요청을 보낼때마다 스레드를 생성하면 성능이 저하되기 때문에 스레드 풀을 사용하여 미리 스레드를 생성해놓고 작업 큐에 요청이 들어오면 스레드를 할당하는 방식을 사용한다.

JAVA에선 ExecutorService, Feature 인터페이스와 FutureTask 클래스를 사용하여서, Spring 에서는 @Async, AsyncRestTemplate, WebClient 등을 사용하는 방법으로 비동기 프로그래밍을 한다. 방식의 차이일 뿐 결국 전부 멀티쓰레드를 이용하여 비동기 프로그래밍을 하는 것이다.


- (4) 메세지 큐를 쓰는 이유에 대하여 2가지 예시를 서술해주세요.

메시지 큐는 비동기식 통신을 지원한다. 즉, 메시지를 생산하고 소비하는 엔드포인트가 서로가 아니라 대기열과 상호 작용한다. 생산자는 요청이 처리되길 기다리지 않고 이를 대기열에 추가할 수 있다. 소비자는 메시지가 제공될 때만 처리한다. 시스템의 어떤 구성 요소도 다른 구성 요소를 기다리느라 지연되지 않으므로 데이터 흐름이 최적화된다.

대기열을 사용하면 데이터가 지속되고 시스템의 서로 다른 부분이 오프라인이 될 때 발생하는 오류를 줄일 수 있다. 서로 다른 구성 요소를 메시지 대기열로 분리함으로써 내결함성을 강화할 수 있다. 시스템의 한 부분에 접속할 수 없더라도 다른 부분이 여전히 대기열과 계속 상호 작용할 수 있다. 대기열 자체 또한 미러링되어 더 뛰어난 가용성을 제공할 수 있다


- (5) 본인이 작성한 서버 코드가 있는 github repo 주소를 제출해주세요. (CRUD 기능을 모두 포함하여야 하며, 서버에 대한 설명을 README에 작성해주시면 더욱 좋습니다.) 
https://github.com/o-rchid/form

- (6 - Optional) 해당 수업을 통해 꼭 배우고 싶은 주제 또는 지식이 있다면 자유롭게 서술해주세요.
