# Caching

## Caching의 개념

- `데이터나 결과를 미리 저장`하여 나중에 `더 빠르게 접근하거나 재사용`할 수 있도록 하는 메커니즘

## Caching의 이점

- 캐시에 저장된 데이터는 `더 빠른 저장소에 위치`하므로 데이터를 직접적으로 가져오는 것보다 더 `빠르게 접근`할 수 있다.
- `반복적으로 동일한 데이터에 접근`하는 작업이 많은 경우, 원본 데이터 저장소에 매번 접근하는 것보다 캐시를 이용하여 `시스템 부하를 줄일` 수 있다.
- 원격 데이터 소스로부터 데이터를 가져오는 `네트워크 트래픽을 줄여`줄 수 있다.

## Caching의 사용 예시

- `웹 브라우저`가 웹 페이지의 이미지, 스크립트, 스타일 시트 등을 `로컬 저장소에 캐싱`하여 다음에 같은 페이지를 방문할 때 더 빠르게 로딩시킨다.
- 캐싱은 `하드웨어와 소프트웨어 모두에서 사용`되며, 프로그래밍에서는 메모리 캐싱, 데이터베이스 쿼리 결과 캐싱, 웹 페이지 캐싱 등 다양한 형태로 활용된다.