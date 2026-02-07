Binary Search Tree: Motivation

Searching in a normal binary tree takes O(n) time
Because you may need to traverse every node
Similar to linear search

In a Binary Search Tree (BST), searching can be done in O(log n)
Same idea as binary search on sorted data
This works because the tree maintains order

---

Binary Search Tree: Definition

A BST is a binary tree that maintains elements in sorted order

Properties
Each node has at most two children
For every node
All elements in left subtree are smaller
All elements in right subtree are larger
This rule applies to every node, not just the root

If any node violates this rule, it is not a valid BST

Important property
Inorder traversal of a BST always produces sorted output

---

Searching in a BST

Idea
Compare target value with current node
If equal: found
If target is smaller: go left
If target is larger: go right
Repeat until found or null

We do not traverse the entire tree
We only follow one path from root to leaf

Time complexity
O(height of tree)
Balanced BST: O(log n)
Worst case skewed tree: O(n)

Iterative search example

```cpp
bool searchBST(TreeNode* root, int key) {
    TreeNode* cur = root;

    while (cur != NULL) {
        if (cur->val == key) return true;
        else if (key < cur->val) cur = cur->left;
        else cur = cur->right;
    }

    return false;
}
```

---

Insertion in a BST

Idea
Find the position where the value should exist
If that spot is empty, insert there
Traversal logic is same as search

Corner case
If root is null, new node becomes root

Steps
Start from root
If value is smaller: go left
If larger: go right
If target child is null: insert node there

Time complexity
O(height)
Balanced: O(log n)

Insertion example

```cpp
TreeNode* insertBST(TreeNode* root, int val) {
    TreeNode* node = new TreeNode(val);

    if (root == NULL) return node;

    TreeNode* cur = root;

    while (true) {
        if (val < cur->val) {
            if (cur->left != NULL) cur = cur->left;
            else {
                cur->left = node;
                break;
            }
        } else {
            if (cur->right != NULL) cur = cur->right;
            else {
                cur->right = node;
                break;
            }
        }
    }

    return root;
}
```

---

Deletion in a BST

First step is always search for the node

There are 3 cases

Case 1: Leaf node
No children
Simply remove it
Return null to parent

Case 2: Node with one child
Replace node with its child
Return the child

Case 3: Node with two children
Find inorder successor
Inorder successor is the leftmost node of right subtree
Copy successor value into node
Delete successor from right subtree

Recursive deletion example

```cpp
TreeNode* deleteNode(TreeNode* root, int key) {
    if (root == NULL) return NULL;

    if (key < root->val)
        root->left = deleteNode(root->left, key);
    else if (key > root->val)
        root->right = deleteNode(root->right, key);
    else {
        if (root->left == NULL) return root->right;
        if (root->right == NULL) return root->left;

        TreeNode* succ = root->right;
        while (succ->left != NULL)
            succ = succ->left;

        root->val = succ->val;
        root->right = deleteNode(root->right, succ->val);
    }

    return root;
}
```

Time complexity
O(height)

---

Balanced vs Unbalanced BST

If tree is skewed
Height becomes n
Operations degrade to O(n)

Balanced BST
Height ≈ log n
Search, insert, delete become efficient

Self balancing trees
AVL trees
B trees
These automatically maintain balance

---

Validating a Binary Search Tree

Goal
Check if a given binary tree follows BST rules

Naive approach
For each node, check entire left and right subtree
O(n²)

Efficient approach
Use range limits

Each node must lie within a valid range
[min, max]

Root range
(-∞, +∞)

For left child
range becomes
[min, root value - 1]

For right child
range becomes
[root value + 1, max]

If node value goes outside range
Tree is invalid

We recursively validate every node

Validation example

```cpp
bool check(TreeNode* root, long long mn, long long mx) {
    if (root == NULL) return true;

    if (root->val < mn || root->val > mx)
        return false;

    return check(root->left, mn, (long long)root->val - 1) &&
           check(root->right, (long long)root->val + 1, mx);
}

bool isValidBST(TreeNode* root) {
    return check(root, LLONG_MIN, LLONG_MAX);
}
```

Time complexity
O(n)
Every node visited once

---

Complexity Summary

Search
Insert
Delete
O(height)
Balanced: O(log n)

Validation
O(n)

Space complexity
Mostly constant for iterative operations
Recursive calls use stack proportional to height
