# Tree

## 1. Tree Definition

- A structure of **unidirectional graph** that resembles a tree with branches extending in all directions from a single root
- A **hierarchical data structure** where data is connected to one or more data directly below it with only one path and one direction
- A **non-linear structure** where multiple data can exist below one piece of data, unlike linear structures that arrange data sequentially
- Tree structures are expressed hierarchically and only branch downward, so there are **no cycles**
- In other words, it can be said to be **a connected graph without cycles**

<br/>

## 2. Tree Structure

- Starts with one vertex data called Root and connects multiple data with **edges**
- Each piece of data is called a **node**, and when two nodes are connected in a parent-child hierarchy, they form a parent/child relationship
- Nodes without children are called **leaf nodes** because they are like leaves on a tree
- Depth
  - The depth from the root to a specific node in a lower hierarchy
  - Root depth is 0
- Level
  - Nodes with the same depth can be grouped and expressed as levels
  - The level of the root with depth 0 is 1
  - Nodes at the same level side by side are called sibling nodes
- Height
  - The height from leaf nodes to the root can be expressed in tree structures
  - Each leaf node's height is set to 0, and parent nodes have a value of +1 to the highest height value of their child nodes
- Subtree
  - A small tree with a tree structure inside a large tree branching from the root of the tree structure
- Real-world Tree Examples
- Computer directory structures, organizational charts, etc.

<br/>

## 2. Binary Tree

- Binary tree characteristics
  - A tree composed of nodes with a maximum of two child nodes
- Classification by data insertion/deletion methods
  - Full binary tree
    - Each node has 0 or 2 child nodes
  - Perfect binary tree
    - A full binary tree that is also a complete binary tree. All leaf nodes have the same level and all levels are completely filled
  - Complete binary tree
    - All nodes except the last level must be completely filled, and nodes in the last level don't need to be completely filled but must be filled from the left

<br/>

## 3. Binary Search Tree

- What is binary search?
  - One of the algorithms for finding a specific value in sorted data
  - An algorithm that divides an array of integers sorted in ascending order into two parts of equal size, then limits the search range to only search in the part where search is needed to find the desired value
- Binary search tree
  - All left child values are smaller than the root or parent, and all right child values are larger than the root or parent
  - Faster search than regular binary trees
  - Even if the value being searched for is not in the tree, the operation and search proceed only up to h times (tree height)

<br/>

## 4. Tree Traversal

- Common characteristics of tree traversal methods
  - All traverse nodes from left to right when visiting
- Tree traversal methods
  - Preorder traversal
    - Starts from the root and sequentially visits left nodes, then moves to right nodes after left node exploration is complete
    - Preorder traversal is mainly used when copying trees
  - Inorder traversal
    - Starts traversal from the leftmost node, and after the traversal of nodes on the left side of the root is complete, moves to nodes on the right through the root to continue exploration
    - Inorder traversal is used to get values in ascending order from binary search trees
  - Postorder traversal
    - Starts traversal from the leftmost node, moves to the right without passing through the root to traverse, then visits the root at the very end
    - Postorder traversal is used when deleting trees. Child nodes must be deleted first before parent nodes can be deleted
  - Level-order traversal
    - Visits nodes based on tree levels rather than based on visiting the root
    - When the root node's level is 1, the level increases as you go down
    - When multiple nodes exist at the same level, nodes are visited in order from left to right
