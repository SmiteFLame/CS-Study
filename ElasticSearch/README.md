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
