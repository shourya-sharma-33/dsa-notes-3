## Topological Sorting

Topological sorting is used on a directed graph.

It gives an ordering of nodes such that
if there is an edge A → B
then A appears before B in the ordering

Multiple valid orderings can exist.

---

## Example intuition

Given 5 nodes
1 2 3 4 5

Dependencies
1 → 2
3 → 1
4 → 5

We should start from nodes that do not depend on any other node.

Nodes with no incoming edges
3 and 4

We can start from either
ordering can change

Possible valid orders
4 3 5 1 2
4 3 1 5 2
and many others

Key idea
always pick nodes with zero dependencies first

---

## Kahn’s Algorithm for Topological Sort

This algorithm is based on indegree.

Indegree
number of incoming edges to a node

Steps

Build adjacency list for directed graph
only add x → y
do not add reverse

Compute indegree array of size n
initialize all to 0

For every edge x → y
increase indegree[y]

Push all nodes with indegree 0 into queue
these are valid starting nodes

While queue is not empty
pop front node
add it to answer

for all adjacent nodes of popped node
decrease their indegree
if indegree becomes 0
push them into queue

At the end
answer vector stores topological order

---

## Detecting impossible case

If graph has a cycle
topological ordering is impossible

Check
if size of answer < number of nodes
then some nodes were never processed
print impossible

Otherwise
print the ordering

---

## C++ implementation

```cpp
vector<int> topoSort(int n, vector<vector<int>>& edges) {
    vector<vector<int>> adj(n);
    vector<int> indegree(n, 0);

    // build graph
    for (auto &e : edges) {
        int x = e[0] - 1;
        int y = e[1] - 1;
        adj[x].push_back(y);
        indegree[y]++;
    }

    queue<int> q;
    vector<int> ans;

    // push zero indegree nodes
    for (int i = 0; i < n; i++) {
        if (indegree[i] == 0)
            q.push(i);
    }

    while (!q.empty()) {
        int node = q.front();
        q.pop();

        ans.push_back(node);

        for (int nei : adj[node]) {
            indegree[nei]--;
            if (indegree[nei] == 0)
                q.push(nei);
        }
    }

    // cycle check
    if (ans.size() < n) {
        cout << "impossible\n";
        return {};
    }

    // convert back to 1-based
    for (int &x : ans) x++;

    return ans;
}
```
