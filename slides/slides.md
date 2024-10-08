---

title: ADS project 1
separator: <!--s-->
verticalSeparator: <!--v-->
theme: league
css: style.css
highlightTheme: tomorrow-night-bright
mathjax: true
revealOptions:
  width: 1520
  height: 950
  margin: 0.04
  transition: 'convex'
  slideNumber: true

---

## ADS 2024 秋冬

## Project 1  Comparing Different Binary Search Trees

- 小组：第7组
- 组长：陆孝本
- 组员：陈子涵，邱俊明
- 汇报日期：October 9，2024
- 指导老师：张国川，何家骏

<!--s-->

## Contents

1. Abstract
2. Analysis of BB[α] Tree
3. Comparison of the binary search trees
4. Experiments
5. Results, Analysis and Conclusion

<!--s-->

## Chapter 1 Abstract

<div style="text-align: left;text-indent: 2em;">

  In this project, we compare four binary search trees: Basic BST, AVL Tree, Splay Tree, BB[α] Tree:

</div>

<div style="text-align: left;">

- **Chapter 2**: Theoretical analysis of BB[α] trees, solving questions from Problem 17-3.
- **Chapter 3**: Theoretical comparison of BST, AVL, Splay, and BB[α] trees.
- **Chapter 4**: Experimental comparison, visualized with graphs.
- **Chapter 5**: Results and conclusion.

</div>

<!--s-->

## Chapter 2 Analysis of BB[α] Tree

<!--s-->

## 2.1 Description

<div style="text-align: left;text-indent: 2em;">

The BB[α] tree is a balanced binary search tree where each node has an additional attribute, `x.size`, representing the total number of nodes in its subtree. A node is α-balanced if both its left and right subtrees have sizes no greater than α × x.size, where α is a constant between 1/2 and 1. The entire tree is considered α-balanced if all nodes meet this condition, ensuring the tree remains balanced and avoids degenerating into a skewed structure.

</div>

<!--s-->

## 2.2 Theoretical Analysis

<!--v-->

### Question 1

<div style="text-align: left; text-indent: 2em; background-color: #0000FF; padding: 10px; color: white;">

**Given a node x in an arbitrary binary search tree, show how to rebuild the subtree rooted at x so that it becomes 1/2-balanced. Your algorithm should run in time Θ(x.size), and it can use O(x.size) auxiliary storage.**

</div>

1. **In-order Traversal**: Perform an in-order traversal of the subtree rooted at node x to store its elements in sorted order. This traversal touches each node three times, giving a time complexity of Θ(x.size).
2. **Rebuilding the Tree**: After storing the elements in a list, rebuild the subtree by selecting the median as the new root. Recursively select medians from the left and right halves of the list to form 1/2-balanced subtrees.
3. **Recurrence and Complexity**: The recurrence for the rebuilding process is T(n) = 2T(n/2) + O(n), which resolves to T(n) = O(n). Thus, the rebuilding takes linear time, Θ(x.size).

<!--v-->

### Question 2

<div style="text-align: left; text-indent: 2em; background-color: #0000FF; padding: 10px; color: white;">

**Show that performing a search in an n-node α-balanced binary search tree takes O(logn) worst-case time.**

</div>

<div style="text-align: left;">

Proof by Induction: Any tree with $\leq\alpha^{-d} + d$ elements has a depth of at most d.
- Base Case (d=0): When \(d = 0\), the tree consists of a single node, so the depth is 0:
$$\alpha^0 = 1$$ Thus, the base case holds.
- Inductive Hypothesis: Assume for depth \(d - 1\), the number of nodes is at most:
$$\alpha^{-(d-1)} + (d - 1)$$ and the depth is at most \(d - 1\).

</div>

<!--v-->

- Inductive Step: For depth d, the α-balance condition gives:
$$\text{root.left.size} \leq \alpha \cdot \text{root.size}$$
This implies the size of the right subtree is:
$$\text{root.right.size} > (1 - \alpha) \cdot \text{root.size} - 1$$
Using this recurrence, we get:
$$\text{root.right.size} > (1 - \alpha) \cdot \alpha^{-d} + d - 1$$
- Thus, the depth is O(log n), completing the inductive proof.

<!--v-->

### Question 3

<div style="text-align: left; text-indent: 2em; background-color: #0000FF; padding: 10px; color: white;">

**Argue that any binary search tree has nonnegative potential and that a 1/2-balanced tree has potential 0.**

</div>

<div style="text-align: left;text-indent: 2em;">

The potential function is defined as the sum of Δ(x) for each node x, where Δ(x) is a nonnegative value. Therefore, the potential is always nonnegative:
$$\Phi = \sum_{x} \Delta(x) \geq 0$$
In a 1/2-balanced tree, Δ(x) ≤ 1 for all nodes, leading to zero nonzero terms in the sum, thus:
$$\Phi = 0$$

</div>

<!--v-->

### Question 4

<div style="text-align: left; text-indent: 2em; background-color: #0000FF; padding: 10px; color: white;">

**Suppose that m units of potential can pay for rebuilding an m-node subtree. How large must c be in terms of α in order for it to take O(1) amortized time to rebuild a subtree that is not α-balanced?**

</div>

<div style="text-align: left;text-indent: 2em;">

To ensure efficient rebuilding, the potential must cover the cost of rebalancing. If a tree becomes unbalanced because the left subtree grows too large, this implies:
$$x.left.size > \alpha \cdot x.size = \left( \alpha - \frac{1}{2} \right) \cdot x.size + \frac{1}{2} \cdot \alpha \cdot x.size$$
Thus, the constant \( c \) must satisfy:
$$c \geq \frac{1}{\alpha - \frac{1}{2}}$$

</div>

<!--v-->

### Question 5

<div style="text-align: left; text-indent: 2em; background-color: #0000FF; padding: 10px; color: white;">

**Show that inserting a node into or deleting a node from an n-node α-balanced tree costs O(logn) amortized time.**

</div>

<div style="text-align: left;text-indent: 2em;">

After inserting or deleting a node, the tree may become unbalanced. The affected node’s ancestors' Δ values change. Rebalancing the tree from the lowest unbalanced node upwards takes constant amortized time per level. Since there are \( O(log n) \) levels, the total amortized time is:
$$
O(\log n)
$$

</div>

<!--s-->

## Chapter 3 Comparison of the binary search trees

<!--s-->

## 3.1 Binary Search Tree (BST)

<!--v-->

### 3.1.1 Description

<div style="text-align: left;text-indent: 2em;">

A Binary Search Tree is a data structure where each node has at most two children, with the left subtree containing values less than the node and the right subtree containing values greater than the node.

</div>

<!--v-->

### 3.1.2 Data Structure

```cpp
typedef struct bstNode* bst;
    struct bstNode{
    int key;
    bst left;
    bst right;
    } bstNode;
```

<!--v-->

### 3.1.3 Operations

<div style="text-align: left;">

- Search: To search for a value in a BST, compare it with the current node. If the value is smaller, proceed to the left child; if larger,proceed to the right child. Repeat until the value is found or a NULL node is reached.
- FindMin/FindMax: To find the minimum/maximum value, traverse the tree from the root to the leftmost/rightmost node. The leftmost/rightmost node contains the smallest/largest value in the BST.
- Insert: To insert a new value, begin at the rootand recursively compare the value with the current node. Traverse left if the value is smaller or right if it is larger. Insert the new node at the first empty position (leaf node).
- Delete: There are three cases for deleting a node:

-- Leaf Node: Simply remove it.

-- Node with One Child: Replace the node with its child.

-- Node with Two Children: Replace the node with its in-order predecessor or successor and recursively delete that node.

</div>

<!--v-->

### 3.1.4 Analysis

<div style="text-align: left;text-indent: 2em;">

Height of the tree: The height of a BST depends on its structure. In the worst case (a skewed tree), the height can be $O(n)$. In the average case, the height is $O(\log n)$, which occurs in balanced trees. 

For basic BST, all the operations have a time complexity of $O(\log n)$.

</div>

<!--s-->

## 3.2 AVL Tree

<!--v-->

### 3.2.1 Description

<div style="text-align: left;text-indent: 2em;">

An AVL tree is a binary search tree with a balance condition. A tree is height-balanced if its left and right subtrees are height-balanced, and the height difference $|h_L - h_R| \leq 1$. The balance factor, $BF(\text{node}) = h_L - h_R$, must be $-1, 0$, or $1$ in an AVL tree, ensuring its balance.

</div>

<!--v-->

### 3.2.2 Data Structure

```cpp
typedef struct avlNode* avl;
    struct avlNode{
        int key;
        avl left;
        avl right;
        int height;
    } avlNode;
```

<!--v-->

### 3.2.3 Unbalanced Cases and Corresponding Operations After Insertion

```
function insert(key, tree):
    # Step 1: Base case - If tree is empty, create a new node
    if tree is NULL:
        create a new node
        set the node's key to the input key
        set left and right children to NULL set height to 0
        return the new node
    # Step 2: Insert key in the left subtree
    if key is less than tree's key:
        recursively insert key into tree's left child
        # Step 2a: Check if the tree is imbalanced on the left
        if height of left subtree - height of right subtree equals 2:
            increment rotation count
            # Perform rotations based on the structure of the subtree
            if key is less than left child's key:
                perform left-left rotation
            else: perform left-right rotation
    # Step 3: Insert key in the right subtree
    else if key is greater than tree's key:
        recursively insert key into tree's right child
        # Step 3a: Check if the tree is imbalanced on the right
        if height of right subtree - height of left subtree equals 2:
            increment rotation count
            # Perform rotations based on the structure of the subtree
            if key is greater than right child's key:
                perform right-right rotation
            else:
                perform right-left rotation
    # Step 4: Update the height of the current node
    set tree's height to the maximum height of its children + 1
    # Step 5: Return the updated tree
    return tree
```

<!--v-->

### Case1: An insertion into the left subtree of the left child of u

- solution:LL rotation

```
function llRotation(node):
    # Step 1: Perform the rotation
    set new to node's left child
    set node's left child to new's right child
    set new's right child to node
    # Step 2: Update the heights
    update node's height to max height of its left and right children + 1
    update new's height to max height of its left child and  height + 1
    # Step 3: Return the new root of the subtree
    return new
```

### Case2: An insertion into the right subtree of the right child of u

- solution:RR rotation

(Cases 1 and 2 are mirror image symmetries with respect to u)

<!--v-->

### Case3: An insertion into the right subtree of the left child of $u$

- solution:LR rotation

```cpp
function lrRotation(node):
    # Step 1: Perform a right-right rotation on the left child
    set node's left child to the result of right-right rotation on node's left child
    # Step 2: Perform a left-left rotation on the current node
    return the result of left-left rotation on the current node
```

### Case4: An insertion into the left subtree of the right child of $u$

- solution:RL rotation

(Cases 3 and 4 are mirror image symmetries with respect to u)

<!--v-->

### 3.2.4 Unbalanced Case and Corresponding Operation After Deletion

```cpp
avl delete(int key, avl tree)
    {
    ...    //similar to the basic BST 
    if(tree != NULL)
        tree->height = max(height(tree->left), height(tree->right)) + 1;
    return balance(tree);
    }
```

<!--v-->

<div style="text-align: left;text-indent: 2em;">

 Case: After deleting a node from an AVL tree, there will be at most one node unbalanced. But after we balance it by rotation, there may be another node unbalanced (an ancestor of the previous unbalanced node).

Solution: We can design a recursive function that finds the node to be deleted through recursion, then updates the balance factors of all its ancestor nodes and rotates unbalanced nodes during backtracking.

</div>

```cpp
 function balance(tree):
    # Step 1: Base case - If tree is empty, return the tree
    if tree is NULL:
        return tree
    # Step 2: Update the height of the current node
    update the height of the tree
    # Step 3: Check if the tree is left-heavy
    if height difference between left and right subtrees is 2:
        # Step 3a: Perform left-left or left-right rotation based on the structure of the left subtree
        if height of left-left subtree is greater than or equal to left-right subtree:
            perform left-left rotation
        else:
            perform left-right rotation
    # Step 4: Check if the tree is right-heavy
    else if height difference between right and left subtrees is -2:
        # Step 4a: Perform right-right or right-left rotation based on the structure of the right subtree
        if height of right-right subtree is greater than or equal to right-left subtree:
            perform right-right rotation
        else:
            perform right-left rotation
    # Step 5: Return the balanced tree
    return tree
```

<!--v-->

### 3.2.5 Analysis

<!--v-->

1.The asymptotic upper bound of AVL tree’s height

<div style="text-align: left;text-indent: 2em;font-size:24px;">

Let $n_k$ be the least nodes of an AVL tree whose height is $h$, then $h \leq f(n_k)$. We can easily conclude that:

$n_k = n_{k-1} + n_{k-2} + 1 \quad (n_0 = 1, n_1 = 2)$

We find it is similar to Fibonacci numbers:

$F_0 = 0, F_1 = 1, F_i = F_{i-1} + F_{i-2} \quad \text{for } i > 1$

So we conclude that:

$n_h = F_{h+3} - 1$

proof:

Base case: For $h = 2$, $n_2 = 4$, $F_5 - 1 = 4$, $n_2 = F_5$.

Inductive hypothesis: For arbitrary $h \geq 2$, assume that for $h \leq k$, $n_h = F_{h+3} - 1$.

Inductive step: When $h = k + 1$:

$n_{k+1} = n_k + n_{k-1} + 1 = F_{k+3} + F_{k+2} - 1 = F_{k+4}$

Thus, we proved that $n_h = F_{h+3} - 1$. So, $n_h \approx F_{i+3} - 1$ and $F_i = O(\log n)$.

Therefore, $h = O(\log n)$. Therefore the asymptotic upper bound of AVL tree’s height is $O(\log n)$.

</div>

<!--v-->

2.The worst time complexity of insertion

<div style="text-align: left;text-indent: 2em;">

An insertion takes the time to find the position to insert and at most one rotation (LL, RR, LR or RL) to balance the AVL tree. So the worst time complexity is:

$O(h) + O(1) = O(\log n)$

</div>

3.The worst time complexity of deletion

<div style="text-align: left;text-indent: 2em;">

A deletion takes the time to find the node to delete and at most $O(h)$ rotations to balance the AVL tree. So the worst time complexity is:

$O(h) + O(h) \cdot O(1) = O(\log n)$

</div>

<!--s-->

## 3.3 Splay Tree

<!--v-->

### 3.3.1 Description

<div style="text-align: left;text-indent: 2em;">

A splay tree is a self-adjusting binarysearch tree that can implement insertion, search, deletion based on splayoperation with amortized logarithmic performance.

</div>

<!--v-->

### 3.3.2 Data Structure

```cpp
typedef struct splayNode* splay;
    struct splayNode{
        int key;
        splay left;
        splay right;
    } splayNode;
    static splay nullNode;
```

<!--v-->

### 3.3.3 The main operation: splay

- Case1: Zig (only perform at most once)

<div style="text-align: center;">

  <img src="image\zig.png" alt="zig" style="width: 500px; display: block; margin: 10px auto;">

</div>

- Case2: Zig-zag

<div style="text-align: center;">

  <img src="image\zig-zag.png" alt="zig-zag" style="width: 500px; display: block; margin: 10px auto;">

</div>

- Case3: Zig-zig

<div style="text-align: center;">

  <img src="image\zig-zig.png" alt="zig-zig" style="width: 500px; display: block; margin: 10px auto;">

</div>

<!--v-->

### 3.3.4 Operations of insertion

-  Step 1: Insert a node as you would in a normal binary search tree.
- Step 2: After insertion, splay the inserted node. As a result, the newly inserted node becomes the root of the tree.

```cpp
function insert(key, tree):
    # Step 1: Create a new node
    create a new node
    set the new node's key to the input key
    # Step 2: Check if the tree is empty
    if tree is nullNode:
        set new node's left and right children to nullNode
        set tree to the new node
    else:
        # Step 3: Splay the tree with the given key
        set tree to the result of splay operation on the key and tree 
        # Step 4: Insert the new node based on the key comparison
        if key is less than tree's key:
            set new node's left child to tree's left child
            set new node's right child to tree
            set tree's left child to nullNode
            set tree to new node
        else if key is greater than tree's key:
            set new node's right child to tree's right child
            set new node's left child to tree
            set tree's right child to nullNode
            set tree to new node
        else if key is equal to tree's key:
            free the new node (duplicate key, so no insertion)
    # Step 5: Return the updated tree
    return tree
```

<!--v-->

### 3.3.5 Operations of deletion

- Step 1: Splay the node named $x$ to be deleted.
- Step 2: Delete $x$ as you would from a normal binary search tree.

<!--v-->

### 3.3.6 Analysis

<div style="text-align: left;font-size:35px;">

We define $\Phi (T) = \sum \log S(i)$ and $R(i) = \log S(i)$ where $S(i)$ is the number of descendants of $i$ (including $i$ itself).

- Zig:

$c_i = 1 + R_2(X) - R_1(X) + R_2(P) - R_1(P) \leq 1 + R_2(X) - R_1(X)$

- Zig-zag:

$c_i = 1 + R_2(X) - R_1(X) + R_2(P) - R_1(P) + R_2(G) - R_1(G) \leq 2 \times (R_2(X) - R_1(X))$

- Zig-zig:

$c_i = 1 + R_2(X) - R_1(X) + R_2(P) - R_1(P) + R_2(G) - R_1(G) \leq 3 \times (R_2(X) - R_1(X))$

We conclude that the amortized time to splay a tree with root $T$ at node $X$ is at most:

$3 \times (R_2(X) - R_1(X)) = O(\log N)$

</div>

<!--s-->

## Chapter 4 Experiments

<!--s-->

## 4.1 Experiment Design

<div style="text-align: left;text-indent: 2em;">

The goal of the experiment is to evaluate and compare the performance of various binary search tree (BST, AVL Tree, Splay Tree and BB[$\alpha$] Tree).

We evaluate the performance of the four types of trees based on the total time cost and the average depth of nodes after N different operations. The operations include sequentially insertion, randomly insertion and randomly insertion or deletion. We also test the height of the trees and track the times that AVL Tree and BB[$\alpha$] Tree become unbalanced. Additionally, we converted recursive functions into non-recursive versions when necessary to avoid stack overflow because the maximum N can be 1000000.

</div>

<!--s-->

## 4.2 Random Data Generation

<div style="text-align: left;text-indent: 2em;font-size:36px;">

To generate random data, we used “rand( )” function, but it can only generate integers between 0 and 32,767. To generate random numbers between 0 and 999,999, we applied the following operation: let the generated random number be x, then shift x left by 15 bits, perform a bitwise or operation with x, and finally take the result modulo 1,000,000. The result will be an integer between 0 and 999,999. 

The random numbers generated by the "rand( )" function are pseudo-random, calculated from a value called the “seed” based on a specific formula, which means that if the random seed is the same, the entry point of the “rand( )” function is the same, then the generated random numbers will also be the same each time. So before calling the “rand( )” function, we used the “srand( )” function to set the random number seed, which can be set by passing in a timestamp to determine the entry point so that avoiding the case that the entry point of the “rand( )” function is the same and we can get really random number.

</div>

<!--s-->

## 4.3 Experiment Results

<!--v-->

### 4.3.1 Comparison of the total time of in order insertions

<!--v-->

[图表 insert inorder total time](graph\1-insert-inorder-total-time.html)

- conclusion: BST is much slower than the other three trees.
- conclusion: AVL Tree, Splay Tree and BB[0.7] Tree is directly proportional to N. (It seems unbelievable, and I will explain it in Chapter5)

[图表 BST insert inorder total time 拟合N²](graph\2-BST-insert-inorder-拟合N².html)

- conclusion: BST’s total time is directly proportional to N².

<!--v-->

### 4.3.2 Comparison of the total time of random insertions

[图表 insert random total time](graph\8-random-insert-total-time.html)

<!--v-->

### 4.3.3 Comparison of the total time of random insertions or deletions

[图表 insert and delete random total time](graph\9-random-insertdelete-total-time.html)

<!--v-->

### 4.3.4 Comparison of the average depth of in order insertions

<!--v-->

[图表 insert inorder average depth](graph\7-insert-inorder-ave-depth.html)

- conclusion: Splay Tree and BST are skewed into linked list.
- conclusion: AVL Tree and BB[0.7] Tree has the similar average node depth.

[图表 insert inorder average depth AVL and BB[0.7] 拟合log(N)](graph\13-insert-inorder-ave-depth拟合.html)

- conclusion: AVL Tree and BB[0.7] Tree‘s average node depth is directly proportional to log(N).

<!--v-->

### 4.3.5 Comparison of the average depth of random insertions

<!--v-->

[图表 insert random average depth](graph\6-random-insert-ave-depth.html)

- conclusion: Splay Tree’s nodes average depth is random.

[图表 insert random average depth BST,AVL,BB[0.7] 拟合log(N)](graph\14-random-insert-ave-depth拟合.html)

- conclusion: The others’ nodes average depth is directly proportional to log(N).

<!--v-->

### 4.3.6 Comparison of unbalance times of in order insertions, random insertions and random insertions or deletions

[图表 in order insertions](graph\10-insert-inorder-unbalanced-time.html)

[图表 random insertions](graph\11-random-insert-unbalanced-time.html)

[图表 random insertions or deletions](graph\12-random-insertdelete-unbalanced-time.html)

<!--s-->

## Chapter 5 Results, Analysis and Conclusion

<!--s-->

## 5.1 Comparison of the total time of in order insertions

<!--v-->

### 5.1.1 Result

<div style="text-align: left;text-indent: 2em;">

The result is that Splay Tree is the fastest, AVL Tree is the second, BB[0.7] Tree is the third and BST is the slowest. And from the Picture 1, 2 and 3, we can find that BST’s total time is directly proportional to N² as we expected, but the other three tree’s total time is directly proportional to N, which is not the same as our expectation.

</div>

<!--v-->

### 5.1.2 The reason why BST’s total time is directly proportional to N²

<div style="text-align: left;text-indent: 2em;">

 When we insert node into a BST in order, each node insertion may traverse down a single path until it finds its appropriate position. This may lead to the tree’s height reaching O(N), where N represents the number of nodes in the tree. Therefore, for nodes whose value in order, the total time complexity of insertion is O(N²).

</div>

<!--v-->

### 5.1.3 The reason why BB[0.7] Tree and AVL Tree’s total time is directly proportional to N but not $N \cdot \log(N)$

<div style="text-align: left;text-indent: 2em;font-size:34px;">

As we all know, both BB[$\alpha$] Tree and AVL Tree are self-balanced trees. When we insert nodes into these two trees in order, the AVL Tree will update the balance factor and rotate the unbalanced node to keep the trees’ depth $O(\log(N))$, and the BB[$\alpha$] tree will rebuild the subtrees that don’t meet the requirement of $\alpha$ to be balanced, so that the trees’ depth can be $O(\log(N))$. 

According to theoretical analysis, it seems the total time should be directly proportional to $N \cdot \log(N)$. To solve the problem, we tested height of the trees. The result is, as the data size increases from 10,000 to 1,000,000, the height of the two types of trees increased slowly (AVL Tree: from 13 to 19; BB[0.7] Tree: from 19 to 27).

Thus, it is not proper to use $O(\log(N))$ to represent the depth of the trees. We can regard the depth as a constant, so that our experiment matches the theory. Additionally, if you still think the total time is directly proportional to $N \cdot \log(N)$, it can also be explained because the situation meets the case of $N \cdot \log(N)$ when the base of the logarithm is large enough.

</div>

<!--v-->

### 5.1.4 The reason why Splay Tree is the fastest and its time is proportional to N

<div style="text-align: left;text-indent: 2em;">

When we insert a node into a Splay Tree in order, for our code implementation (referred from Data Structure and Algorithm Analysis), the node is inserted as the root of the tree and it only takes $O(1)$ time with no rotation. Thus, the total complexity is $O(N)$, and the performance is the best, apparently.

</div>

<!--s-->

## 5.2 Comparison of the total time of random insertions

## (random insertion or deletion case is similar to it)

<!--v-->

### 5.2.1 Result

<div style="text-align: left;text-indent: 2em;">

The result is that the BST is the fastest and the AVL Tree is the slowest. When the data size is small, Splay Tree is faster than BB[0.7] Tree, but when the data size gets larger, BB[0.7] Tree runs better than Splay Tree. The reason why BST, AVL Tree, and Splay Tree’s total time is directly proportional to N is the same as in the order insertion case.

</div>

<!--v-->

### 5.2.2 The reason why BST is better than the other three trees

<div style="text-align: left;text-indent: 2em;">

In our experiment, the height of the AVL Tree, BB[0.7] Tree, and BST, along with the average depth of their nodes, are quite similar (BST has only slightly more depth than the other two trees). However, the reason why the BST performs better than the AVL Tree and BB[0.7] Tree is due to the fact that both the AVL Tree and BB[0.7] Tree require additional time to maintain their self-balancing property. This balancing process takes extra time, which outweighs the small benefit of reduced depth.

For the Splay Tree, while its amortized time complexity for a single operation is $O(\log N)$, its actual performance can vary significantly depending on the sequence of operations. In cases that require frequent access to recently accessed elements, Splay Trees can perform well. However, for general use, the BST’s simpler structure and lower maintenance make it more efficient compared to the Splay Tree.

</div>

<!--v-->

### 5.2.3 The reason why Splay Tree’s total time is directly proportional to N

<div style="text-align: left;text-indent: 2em;">

According to theoretical analysis, it seems that the total time should be directly proportional to $N \cdot \log(N)$. To solve the problem, we also tested the height of the Splay Tree. The result is that as the data size increased from 10,000 to 1,000,000, the height of the Splay Tree changed slowly (from 44 to 61). So, in that case, it is not proper to use $O(\log N)$ to represent the depth of the trees and the rotations for an insertion or deletion, as we can regard the depth and the rotations as constants so that our experiment meets the theory.

</div>

<!--s-->

## 5.3 Comparison of the average depth of in order insertions

<!--v-->

### 5.3.1 Result

<div style="text-align: left;text-indent: 2em;">

The result is that BST and Splay Tree are skewed into a linked list, and the average depth is directly proportional to N, while the average depth of AVL Tree and BB[0.7] Tree is directly proportional to $\log(N)$. The result quite meets our expectations.

</div>

<!--v-->

### 5.3.2 Average Depth of BST

<div style="text-align: left;text-indent: 2em;">

As in in-order insertion, the tree is skewed into a linked list. As a result, the average depth of nodes becomes directly proportional to N.

</div>

### 5.3.3 Average Depth of Splay Tree

<div style="text-align: left;text-indent: 2em;">

Similar to a regular BST, a Splay Tree can also become skewed into a linked list when nodes are inserted in order. Although Splay Trees are self-adjusting and perform rotations to move frequently accessed nodes closer to the root, after an in-order insertion, the tree still results in a degenerate form.

</div>

<!--v-->

### 5.3.4 Average Depth of Splay Tree

<div style="text-align: left;text-indent: 2em;">

The AVL Tree is a self-balancing binary search tree that maintains a strict balance condition: the heights of the two child subtrees of any node differ by at most one. This balance condition is enforced after every insertion through a series of rotations that keep the tree balanced. As a result, even when nodes are inserted in order, the AVL Tree remains balanced, and the depth of nodes is constrained to $O(\log N)$. The average depth of nodes in an AVL Tree is also proportional to $\log(N)$.

</div>

### 5.3.5 Average Depth of BB[0.7] Tree

<div style="text-align: left;text-indent: 2em;">

The BB[$\alpha$] Tree is another type of balanced binary search tree, where the balance factor is allowed to be slightly more relaxed than in an AVL Tree. Specifically, the BB[0.7] Tree permits a slightly larger height difference between subtrees compared to the strict AVL balance condition, but it still maintains a reasonably balanced structure. As a result, the average depth of nodes in the BB[0.7] Tree remains proportional to $\log(N)$.

</div>

<!--s-->

## 5.4 Comparison of the average depth of random insertions

<!--v-->

### 5.4.1 Result

<div style="text-align: left;text-indent: 2em;">

The result is that the average depth of BST, AVL Tree, and BB[0.7] Tree is directly proportional to $\log(N)$. The average node depth of a Splay Tree fluctuates within a certain range. The analysis of AVL Tree and BB[0.7] Tree is similar to the in-order insertion case.

</div>

<!--v-->

### 5.4.2 Average Depth of BST

<div style="text-align: left;text-indent: 2em;">

For a BST with random insertions, the average node depth can still be expected to follow a logarithmic trend under ideal conditions. This is because with random insertions, the tree maintains a roughly balanced structure, even though there is no guarantee of perfect balance.

</div>

### 5.4.3 Average Depth of Splay Tree

<div style="text-align: left;text-indent: 2em;">

The Splay Tree, unlike the AVL and BB[0.7] Trees, exhibits a fluctuating average depth when random insertions are performed. This fluctuation is due to the self-adjusting behavior of the tree, which moves frequently accessed nodes closer to the root through a series of rotations.

</div>

<!--s-->

## 5.5 Comparison of unbalance times of in order insertions, 

## random insertions and random insertions or deletions

## (Only AVL Tree and BB[0.7] Tree)

<!--v-->

<div style="text-align: left;text-indent: 2em;">

The result is that AVL Tree’s unbalanced times is larger than BB[α] Tree. This is due to the balancing condition of the AVL Tree is stricter than that of the BB[0.7] Tree, which means AVL Tree is more easy to become unbalanced.

</div>

<!--s-->

## Thank you for listening!
