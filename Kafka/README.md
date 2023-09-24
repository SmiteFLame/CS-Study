# Kafka

LinkedIn에서 개발한 분산 메시징 시스템으로 대용량 실시간 로그처리에 특화된 아키텍처 설계를 통하여 기존 메시징 시스템보다 우수한 TPS를 보여준다.

## 특징

- 분산 스트리밍 플랫폼
- 데이터 파이프 라인 구성시, 주로 사용되는 오픈소스 솔루션
- 대용량의 실시간 로그처리에 특화되어 있는 솔류션
- 데이터 유실없이 안적하게 전달하는 것이 주목적인 메시지 시스템
- 클러스티링이 가능하므로, Fault-Tolerant한 안정적인 아키텍처와 빠른 퍼포먼스로 데이터처리
- 수평적으로 서버의 Scale-Out이 가능함
- pub-sub 모델의 메시지 큐

### 구성 요소

- Event: Consumer가 데이터를 주고 받는 단위
- Producer: 이벤트를 게시(Post)하는 클라이언트 어플리케이션을 의미한다.
- Consumer: 이러한 Topic을 구독하고 이로 부터 얻어낸 Event를 처리하는 클라이언트 어플리케이션
- Topic: Event가 쓰이는 곳, Producer는 이 Topic에 Event를 게시한다.
  - Consumer는 Topic으로 부터 이벤트를 가져와 처리한다.

### 브로커

브로커는 카프카 서버라고도 불린다.

- 브로커 내부에 여러 토픽들을 생성될 수 있고 이러한 토픽들에 의해 생성된 파티션들이 보관하는 데이터에 대해 분산 저장해주거나 장애 발생시, 안전하게 데이터를 보관할 수 있도록 도와주는 역할
- 클라언트와 데이터를 주고 받기 위해 사용되는 주체로, 데이터를 분산 저장하여 장애가 발생하더라도 안전하게 사용할 수 있도록 도와주는 애플리케이션
- 여러대를 구성하여, 클러스터로 묶어서 운영할 수 있다.

1. 데이터 전송: 프로듀서로 부터 데이터를 받으면 카프카 브로커는 프로듀서가 요청한 토픽의 파티션에 데이터를 저장하고 컨슈머가 데이터를 요청하면 파티션에 저장된 데이터를 전달한다.
2. 데이터 복제, 동기화: 클러스터로 묶은 브로커 중 일부가 장애가 발생하더라도 데이터를 유실하지 않고 안전하게 사용할 수 있도록 복제

### Replication

안정성을 높이기 위해 각 메시지들을 여러 개로 복제하여 카프카 클러스터 내 브로커들에 분산시키는 동작

### 파티션

- 하나의 토픽을 여러 개의 논리적인 개념이 파티션으로 나누어 병렬 처리가 가능하도록 한다
- 이러한 파티션을 이용해 분산 처리할 수 있다.

## Kafka Consumer 구성
- 모든 Consumer는 고유한 Group Id를 가지는 Consumer Group에 소속
- 한 Consumer Group 내에서 한 Consumer는 여러 Partition은 읽을 수 있다.
  - 한 Partition을 여러 Consumer가 읽을 수 없다.

### Kafka가 Message 읽을 때 순서
- Subscribe
  - Broker으로 부터 읽어오고자 하는 토픽을 설정한다. 
- Poll
  - 주기적으로  브로커의 Topic Partition에서 메시지를 가져온다.
  - 최초 Poll은 브로커로 부터 Meta 정보를 가져오고 Group Coorditionator에 Join 한다.
  - Batch 단위로 메시지를 가져온다.
- Commit을 이용하여 Broker의 내부 토픽인 Consumer Offset에 이 Topic + Partition이 다음 읽을 Offset의 위치를 기록 한다.

### Kafka의 구성
1. Fetcher
2. ConsumerNetworkClient
3. ConsumerCoordinator
4. HeartBeatThread
5. SubscriptionState

#### Fetcher
- poll() 메서드를 통해서 Broker 로부터 메시지를 받아온다.

- Fetcher는 ConsumerNetworkClient의 LinlkedQueue를 가지고 있고 이 곳에서 데이터를 읽어 Parsing 한 후, 본인의 Completed Fetcher에 저장한다.

 

##### Fetcher Parameter
<b>fetch.min.bytes</b><br>
<b>fetch.max.wait.ms</b><br>
<b>fetch.max.bytes</b><br>
<b>max.partition.fetch.bytes</b><br>
<b>max.poll.records</b>: Fetcher가 LinkedQueue에 한 번에 가져올 수 있는 Record (Default: 500)

 

####  Heartbeat Thread
- 백그라운드로 동작하며 끊임없이 Broker에게 Consumer의 상태를 알려준다.
- Broker는 Consumer가 죽었다고 판단되면 리밸런싱 한다.
- Heartbeat Thread는 Consumer가 첫번째 poll()을 수행했을 때 생성된다.

##### Heartbeat Thread Parameter
<b>heartbeat.interval.ms(Default: 3,000)</b> : Heartbeat Thread가 Heartbeat API를 보내는 간격<br>
<b>session.timeout.ms(Default: 45,000)</b>: Broker가 Heartbeat가 기다리는 최대 시간<br>
Broker가 해당 시간 동안 Heartbeat 받지 못하면 Rebalancing 명령 날림<br>
<b>max.poll.interval.ms(Default : 300,000)</b>: 이전 poll() 호출 후, 다음 poll() 호출까지 Broker가 기다리는 시간

- 이 시간동안 poll() 호출이 이루어지지 않으면 Consumer는 Rebalancing 명령 날림


### Consumer Reblanceing 발생한 이유
1. 메세지 Lag이 쌓이게 됨
2. Consumer 1개의 Pod에서 메세지 500개를 poll 함
     - max.poll.records: 500
3. max.poll.interval.ms 시간 내로 메세지 500개 모두 처리 못함 
     - max.poll.interval.ms: Default: 5분
4. Consumer Rebalancing
5. Offset Commit이 진행되지 않음 모두 진행되지 않음
7. 다른 컨슈머에서 마지막으로 커밋된 메세지부터 처리(중복 메세지 처리)
