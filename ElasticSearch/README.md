# Elastic Search

Apache Lucene 기반의 Java 오픈 소스 분산 검색 엔진

- 라이브러리를 단독으로 사용할 수 있으며, 방대한 양의 데이터를 거의 NRT으로 저장, 검색, 분석 할 수 있다.

## ELK 구조

- Logstash: 다양한 소스(DB, csv 파일)의 로그 또는 트랜잭션 데이터를 수집, 집계, 파싱하여 Elastic Search으로 전달
- ElasticSearch: Logstash으로 부터 받은 데이터를 검색 및 집계를 하여 필요한 관심 있는 정보를 획득
- Kibana: ElasticSearch의 빠른 검색을 통해 데이터를 시각화 및 모니터링

## RDBMS와 비교

- Database -> Indx
- Table -> Type
- Column -> Field
- Document -> Row
- SQL -> Query DSL

## Elastic Search 아키텍처

### Cluster

- 가장 큰 시스템 단위, 최소 하나 이상의 노드로 이루어진 노드들의 집합
- 서로 다른 클러스터는 데이터의 접근, 교환을 할 수 없는 독립적인 시스템으로 유지
- 여러대의 서버가 하나의 클러스터 혹은 하나의 서버에 여러 갱의 클러스타 존재
