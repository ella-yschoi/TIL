# Graph

## 1. Graph의 구조

- 직접적인 관계가 있는 경우, 두 점 사이를 이어주는 선이 있음
- 간접적인 관계라면 몇 개의 점과 선에 걸쳐 이어짐
- 하나의 점을 그래프에서는 정점(vertex)라고 표현, 하나의 선을 간선(edge)라고 함

<br/>

## 2. Graph의 표현 방식

- 인접 행렬
  - 두 정점을 바로 이어주는 간선이 있다면 이 두 정점은 인접하다고 말함
  - 서로 다른 정점들이 인접한 상태인지를 표시한 행렬로 2차원 배열의 형태로 나타냄
- 인접 리스트
  - 각 정점이 어떤 정점과 인접하는지 리스트 형태로 표현

<br/>

## 3. 알아두어야 할 Graph 용어들

- 정점(vertex)
  - 노드라고도 하며, 데이터가 저장되는 그래프의 기본 원소
- 간선(edge)
  - 정점 간의 관계(정점을 이어주는 선)
- 인접 정점(adjacent vertex)
  - 하나의 정점에서 간선에 의해 직접 연결된 정점
- 가중치 그래프 (weighted Graph)
  - 연결의 강도가 얼마나 되는지 적혀 있는 그래프
- 비 가중치 그래프 (unweighted Graph)
  - 연결의 강도가 적혀 있지 않은 그래프
- 무향(무방향) 그래프 (undirected graph)
- 진입차수 (in-degree) / 진출차수 (out-degree)
  - 한 정점에 진입하고 진출하는 간선이 몇 개인지 나타냄
- 인접 (adjacency)
  - 두 정점 간에 간선이 직접 이어져 있다면 이 두 정점은 인접한 정점
- 자기 루프 (self loop)
  - 정점에서 진출하는 간선이 곧바로 자기 자신에게 진입하는 경우 자기 루프를 가졌다라고 표현
  - 다른 정점을 거치지 않는다는 것이 특징
- 사이클(cycle)
  - 한 정점에서 출발하여 다시 해당 정점으로 돌아갈 수 있는 경우

<br/>

## 4. BFS와 DFS

- BFS(Breadth-First Search)
  - 너비를 먼저 탐색하는 방법을 Breadth-First Search, 너비 우선 탐색이라고 함
  - 주로 두 정점 사이의 최단 경로를 찾을 때 사용
- DFS(Depth-First Search)
  - 한 정점에서 시작해서 다음 경로로 넘어가기 전에 해당 경로를 완벽하게 탐색할 때 사용
  - BFS보다 탐색 시간은 조금 오래 걸릴지라도 모든 노드를 완전히 탐색 가능
