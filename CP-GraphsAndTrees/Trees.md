## Trees Introduction

A tree is a data structure.

Properties of a tree
non linear data structure
hierarchical structure
has a root node
parent child relationship
no cycles
if a tree has n nodes
it has n minus 1 edges
edges are directed from parent to child

Tree is a special form of graph
with extra constraints

Basic components
nodes: store values
edges: connect nodes

Used in real life
folder structures
hierarchical relationships
organizational trees

---

## Binary Tree

A binary tree is a tree
where each node has at most 2 children

Children are labeled
left child
right child

Each node contains
data
pointer to left child
pointer to right child
missing child is null

Example node structure

```cpp
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int val) {
        data = val;
        left = right = NULL;
    }
};
```

---

## Types of Binary Trees

### Full Binary Tree

Every node has either
0 children
or 2 children

No node has exactly 1 child

---

### Perfect Binary Tree

A perfect tree is also full

Extra rule
all leaf nodes are at the same level

All levels are completely filled

---

### Complete Binary Tree

Levels are filled left to right

During level order traversal
there should be no gaps between nodes

Last level can be incomplete
but nodes must be as left as possible

---

### Degenerate Binary Tree

Each node has only 1 child

Looks like a linked list

Special cases
left skewed tree
all children on left

right skewed tree
all children on right

---

## Height and Depth of a Tree

Two important concepts
height
depth

Depth
measured from root downward
root depth is 0
increases as we go down

Height
measured from node to deepest leaf
leaf height is 0
increases upward

Overall tree height
equals maximum depth

For a specific node
height and depth are different

---

## Balanced Binary Tree

A binary tree is balanced if
for every node

difference between height of
left subtree and right subtree

is either
0 or 1

Important rule
balance must hold for every node
not just the root

If any node violates the rule
tree is not balanced

Adding or removing nodes
can restore balance

---

## Transition to Traversals

Next topic
tree traversal

Goal
how to visit every node in a tree

Multiple traversal algorithms exist
each with a different visiting order

This is the foundation
for solving most tree problems


**Tree Traversal: Introduction**

Tree traversal means visiting all nodes of a tree in a specific order.

Question
How can we traverse a binary tree?

There are multiple traversal algorithms designed for this purpose. Each traversal defines a different visiting order and is useful in different scenarios. Tree traversal is a core and important concept in binary trees.



**Tree Traversal Algorithms: Overview**

There are multiple tree traversal algorithms.

The main recursive traversals
Preorder traversal
Inorder traversal
Postorder traversal

An additional traversal
Level order traversal
This is done using iteration and a queue
It is similar to Breadth First Search (BFS)

Traversal means visiting all nodes of the tree.
All traversals visit every node.
The difference is only the visiting order.

---

**Preorder Traversal**

Order
Root → Left subtree → Right subtree

Idea
Visit the root first
Then recursively traverse the entire left subtree
Then recursively traverse the entire right subtree

Manual shortcut idea
Imagine drawing a line on the left side of each node
Start from root and trace around the tree
Each time you cross a node line, record it
This helps in manual preorder extraction

Recursive logic
If root is null: return
Add root value to answer
Call preorder on left
Call preorder on right

Code example: Preorder (C++)

```cpp
vector<int> ans;

void preorder(Node* root) {
    if (root == NULL) return;

    ans.push_back(root->data);
    preorder(root->left);
    preorder(root->right);
}
```

Time complexity
O(n) where n is number of nodes

---

**Inorder Traversal**

Order
Left subtree → Root → Right subtree

Idea
First go completely left
Then visit root
Then go right

Manual shortcut idea
Draw the line through the middle of each node
Trace and record crossings
This gives inorder sequence

Recursive logic
If root is null: return
Call inorder on left
Add root value
Call inorder on right

Code example: Inorder (C++)

```cpp
vector<int> ans;

void inorder(Node* root) {
    if (root == NULL) return;

    inorder(root->left);
    ans.push_back(root->data);
    inorder(root->right);
}
```

Time complexity
O(n)

---

**Postorder Traversal**

Order
Left subtree → Right subtree → Root

Idea
Root is processed last
First complete left
Then complete right
Then visit root

Manual shortcut idea
Similar tracing trick
But record node after finishing both sides

Recursive logic
If root is null: return
Call postorder on left
Call postorder on right
Add root value

Code example: Postorder (C++)

```cpp
vector<int> ans;

void postorder(Node* root) {
    if (root == NULL) return;

    postorder(root->left);
    postorder(root->right);
    ans.push_back(root->data);
}
```

Time complexity
O(n)

These three traversals are structurally the same
Only the ordering of operations changes

---

**Level Order Traversal**

Idea
Traverse tree level by level
Top to bottom
Left to right

This traversal is equivalent to BFS on a tree
Uses a queue

Steps
Insert root into queue
While queue is not empty
Remove front node
Insert its children into queue
Record nodes level by level

Level-wise traversal trick
Use queue size to know how many nodes are in current level
Process exactly that many nodes
Their children form the next level

Code example: Level order (C++)

```cpp
vector<vector<int>> levelOrder(Node* root) {
    vector<vector<int>> ans;
    if (root == NULL) return ans;

    queue<Node*> q;
    q.push(root);

    while (!q.empty()) {
        int size = q.size();
        vector<int> level;

        for (int i = 0; i < size; i++) {
            Node* cur = q.front();
            q.pop();

            level.push_back(cur->data);

            if (cur->left) q.push(cur->left);
            if (cur->right) q.push(cur->right);
        }

        if (!level.empty())
            ans.push_back(level);
    }

    return ans;
}
```

Time complexity
O(n)

Space complexity
O(n) because queue may store many nodes

---

**Complexity Summary**

All traversals visit each node once
Time complexity for all traversals
O(n)

Extra space
Recursive traversals mainly use recursion stack
Level order additionally uses queue
Queue space can be O(n)


