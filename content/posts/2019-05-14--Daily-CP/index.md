---
title: Daily CP - 14 May 2019
subTitle: Daily discussion of problems solved
category: competitive-programming
cover: dailycp.jpg
menuTitle: competitive-programming
---

## Problem - [Tywin Tactics](https://www.codechef.com/COOK35/problems/TYTACTIC)

#### [Official Editorial](https://discuss.codechef.com/t/tytactic-editorial/2408)

### Problem Description

You are given a tree consisting of n nodes and m edges. Each node in the tree will have a certain skill-level associated with it.

Now you are given two types of queries to compute on - 

Type 1 - Given a node S find the sum of the strengths of all the nodes in the subtree of the node.

Type 2 - Update the strength of a node U with value x

## Naive Approach

Query type 1 - We can perform a dfs in the entire tree with root as index 0. We can then recursively update the strength value of the childrens of a particular node and then print the answer of our query node. Complexity - `O(n)`

Code

```cpp
// n = number of nodes in the tree.
int strength[n]; // given as input
int subtreeStrength[n];
bool visited[n];

void reset() {
  for (int i = 0; i < n; i++) {
    visited[i] = 0;
    subtreeStrength[i] = 0;
  }
}

void dfs(int index)
{
    visited[index] = 1;
    subtreeStrength[index] += strength[index]; // add the node's own strength to the subtreeStrength array
    for (ll i = 0; i < v[index].size(); i++) {
	int child = v[index][i];
	if (!visited[child]) {
	    dfs(child);
	    subtreeStrength[index] += subtreeStrength[child]; // update the subtreeStrength of the node at index with the subtreeStrength of it's child
	}
    }
}
```

Query type 2 - Update the strength with the corresponding value. Complexity - `O(constant)`

The total complexity will be `O(qn)` at worst case. Here n is `100,000` and q is also `100,000` so our solution will definitely get a TLE from the judge.

## Better Approach

Update the strength of a certain node S to x.

Now let's assume if we were given a linear array instead of a tree. If that was the case then we could simply use a segment tree data structure to solve both the queries (query a range and upadte a point) in `O(log n)`.

So if we could find a way to linearize a tree into an array we could then build the segment tree on top of the tree to solve this problem.

### Linearizing the tree data structure - 

If you notice the DFS of a tree closely you will notice that once you call the `dfs()` with a certain index then the point it's called is when you first encounter the node with that index. In the entirety of the for loop you will always be dealing with all the nodes which are only in the subtree of the node. And once the for loop is completely over then you actually get out of the nodes's subtree and the node.

#### Example

Step 1 - Enter a node

Step 2 - Traverse all the children of the node

Step 3 - Exit the node

Let's assume we have a tree like this

![Tree](https://i.imgur.com/FgHKNzW.png)


Let's see how function call works

```cpp
void dfs(int index){
    cout << "Entering the node for index " << index << endl; 
    visited[index] = 1;
    nodeInstant[index].first = instant;
    for(int i = 0; i < v[index].size(); i++){
        int child = v[index][i];
        if(!visited[child]){
            instant++;
            dfs(child);
        }
    }
    nodeInstant[index].second = instant;
}
```


Definitions

Subtree - A 'subtree' of a tree T is a tree consisting of a node in T and all of its descendants in T