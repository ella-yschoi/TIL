# Graph

## 1. Graph Structure

- When there is a direct relationship, there is a line connecting two points
- If it's an indirect relationship, it connects through several points and lines
- A single point is called a vertex in graph theory, and a single line is called an edge

<br/>

## 2. Graph Representation Methods

- Adjacency Matrix
  - If there is an edge directly connecting two vertices, these two vertices are said to be adjacent
  - A matrix showing whether different vertices are in an adjacent state, represented as a 2D array
- Adjacency List
  - Each vertex expresses which vertices it is adjacent to in list form

<br/>

## 3. Important Graph Terms to Know

- Vertex
  - Also called a node, it is the basic element of a graph where data is stored
- Edge
  - The relationship between vertices (lines connecting vertices)
- Adjacent Vertex
  - A vertex directly connected by an edge from one vertex
- Weighted Graph
  - A graph where the strength of the connection is written
- Unweighted Graph
  - A graph where the strength of the connection is not written
- Undirected Graph
- In-degree / Out-degree
  - Indicates how many edges enter and exit a vertex
- Adjacency
  - If two vertices are directly connected by an edge, these two vertices are adjacent vertices
- Self Loop
  - When an edge exiting a vertex immediately enters the vertex itself, it is said to have a self loop
  - The characteristic is that it doesn't pass through other vertices
- Cycle
  - When it's possible to start from one vertex and return to that vertex

<br/>

## 4. BFS and DFS

- BFS (Breadth-First Search)
  - The method of searching breadth first is called Breadth-First Search
  - Mainly used when finding the shortest path between two vertices
- DFS (Depth-First Search)
  - Used when starting from one vertex and completely exploring that path before moving to the next path
  - Although it may take a bit longer than BFS, it can completely explore all nodes
