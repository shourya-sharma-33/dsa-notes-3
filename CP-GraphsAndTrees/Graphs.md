## What is a Graph

A graph is a non linear data structure made of nodes and edges connecting them.

Definition
A graph is a collection of nodes that store data and are connected to other nodes.

Key difference from trees
Trees have strict rules
hierarchical structure
single root
n nodes have n − 1 edges
no cycles
always connected

Graphs have no such restrictions
can have cycles
can be disconnected
no root requirement
no fixed edge count rule

A graph can even contain isolated nodes that are not connected to others.

Examples of real life graphs
social media networks: profiles are nodes, follow/block relationships are edges
Google Maps: locations are nodes, roads with distance/time/traffic are weighted edges

Graphs store this structure and algorithms compute shortest paths and optimal routes.

---

## Basic Graph Terminology

Vertices: nodes that store data
Edges: connections between nodes
Adjacent nodes: two nodes connected by an edge
Path: a route from one node to another through edges

---

## Types of Graphs

### Undirected graph

Edges have no direction
If A is connected to B, you can go both A → B and B → A

### Directed graph

Each edge has a direction
You can only move in the specified direction

### Weighted graph

Each edge has a weight
Weight can represent distance, time, cost, traffic, etc.

Graphs can be directed + weighted or undirected + weighted.

---

## Graph Representation

Graphs are not naturally organized like trees, so we need structures to store them.

Three main representations

### 1. Set of vertices and edges

Graph is stored as
list of vertices
list of edges as pairs (u, v)

Example
vertices: {0, 1, 2, 3}
edges: (0,1), (0,2), (0,3), (1,2)

This directly defines the graph structure.

---

### 2. Adjacency List

Most common representation.

Idea
For each node, store a list of all adjacent nodes.

Implementation concept
array of vectors or list of lists
index represents node
vector at index stores its neighbors

Steps to build adjacency list
create array of size n
for each edge (x, y)
add y to list[x]
add x to list[y] for undirected graph

Example C++ code

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, e;
    cin >> n >> e;

    vector<vector<int>> adj(n);

    for (int i = 0; i < e; i++) {
        int x, y;
        cin >> x >> y;

        adj[x].push_back(y);
        adj[y].push_back(x); // remove for directed graph
    }

    // print adjacency list
    for (int i = 0; i < n; i++) {
        cout << i << ": ";
        for (int v : adj[i]) {
            cout << v << " ";
        }
        cout << endl;
    }
}
```

For weighted graphs
store pairs (neighbor, weight) instead of just neighbor.

---

### 3. Adjacency Matrix

2D matrix of size n × n

matrix[i][j]
1 or weight if edge exists
0 or −1 if no edge

Undirected graph
matrix[i][j] = matrix[j][i]

Directed graph
only one direction is filled

Example C++ code

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, e;
    cin >> n >> e;

    vector<vector<int>> mat(n, vector<int>(n, 0));

    for (int i = 0; i < e; i++) {
        int x, y;
        cin >> x >> y;

        mat[x][y] = 1;
        mat[y][x] = 1; // remove for directed graph
    }

    // print matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << mat[i][j] << " ";
        }
        cout << endl;
    }
}
```

Weighted version
replace 1 with the edge weight.

---

## Why adjacency list or matrix is used

Most algorithms like BFS, DFS, Dijkstra do not operate directly on raw edge lists.
Adjacency structures make it easy to

find neighbors of a node
check if an edge exists
iterate efficiently over connections

Adjacency list: memory efficient for sparse graphs
Adjacency matrix: fast edge lookup, useful for weighted graphs

---

Next topic
Graph traversals: BFS and DFS.


## Graph Traversal Overview

Traversal means visiting all nodes of a graph.

Goal of traversal
go through the entire graph
ensure all reachable nodes are covered

Unlike tree traversals
graphs do not have a fixed ordering like preorder or postorder
order depends on
starting node
method used
data structure used internally

Two main graph traversals
Breadth First Search BFS
Depth First Search DFS

They differ in behavior
BFS explores level by level
DFS explores depth first

---

## Breadth First Search BFS

BFS visits nodes layer by layer.

Key idea
use a queue
track visited nodes to avoid repetition

This is similar to level order traversal in trees.

Steps of BFS
start from a source node, usually 0
push it into queue
mark it visited
repeat while queue is not empty
take front node
visit all its unvisited neighbors
push them into queue
mark them visited

Visited array prevents infinite loops in cyclic graphs.

Important note
If the graph is disconnected, running BFS from only one node will not cover all nodes.
You must start BFS from every unvisited node to cover all components.

Example BFS code using adjacency list

```cpp
vector<int> bfs(int n, vector<vector<int>>& adj) {
    vector<bool> visited(n, false);
    vector<int> result;
    queue<int> q;

    q.push(0);
    visited[0] = true;

    while (!q.empty()) {
        int node = q.front();
        q.pop();

        result.push_back(node);

        for (int nei : adj[node]) {
            if (!visited[nei]) {
                visited[nei] = true;
                q.push(nei);
            }
        }
    }

    return result;
}
```

To handle disconnected graphs

```cpp
for (int i = 0; i < n; i++) {
    if (!visited[i]) {
        run bfs from i
    }
}
```

---

## Depth First Search DFS

DFS goes as deep as possible before backtracking.

Key idea
use stack behavior
can be implemented using
explicit stack
recursion

DFS nature
follow one path fully
then return and explore remaining paths

---

## DFS using stack

Replace queue with stack
front becomes top
behavior becomes depth first

Basic logic
push start node
while stack not empty
pop top
if not visited
mark visited
process node
push neighbors

Example iterative DFS

```cpp
vector<int> dfs_iter(int n, vector<vector<int>>& adj) {
    vector<bool> visited(n, false);
    vector<int> result;
    stack<int> st;

    st.push(0);

    while (!st.empty()) {
        int node = st.top();
        st.pop();

        if (visited[node]) continue;

        visited[node] = true;
        result.push_back(node);

        for (int nei : adj[node]) {
            if (!visited[nei]) {
                st.push(nei);
            }
        }
    }

    return result;
}
```

---

## DFS using recursion

This is the most common implementation.

Idea
visit node
mark visited
recursively visit all unvisited neighbors

Recursive DFS

```cpp
void dfs_rec(int node, vector<vector<int>>& adj,
             vector<bool>& visited) {

    visited[node] = true;
    cout << node << " ";

    for (int nei : adj[node]) {
        if (!visited[nei]) {
            dfs_rec(nei, adj, visited);
        }
    }
}
```

Call it as

```cpp
vector<bool> visited(n, false);
dfs_rec(0, adj, visited);
```

For disconnected graphs
run DFS from every unvisited node.

---

