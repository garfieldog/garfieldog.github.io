title: Leetcode解题-Clone Graph
date: 2015-09-18 10:13:32
tags: [Leetcode, Graph, DFS]
categories: [编程题]
---

## 描述
> Clone an undirected graph. Each node in the graph contains a label and a list of its neighbors.
>
> OJ's undirected graph serialization:
> Nodes are labeled uniquely.
>
> We use # as a separator for each node, and , as a separator for node label and each neighbor of the node.
> As an example, consider the serialized graph {0,1,2#1,2#2,2}.
>
> The graph has a total of three nodes, and therefore contains three parts as separated by #.
>
> First node is labeled as 0. Connect node 0 to both nodes 1 and 2.
> Second node is labeled as 1. Connect node 1 to node 2.
> Third node is labeled as 2. Connect node 2 to node 2 (itself), thus forming a self-cycle.
> Visually, the graph looks like the following:
>
>        1
>       / \
>      /   \
>     0 --- 2
>          / \
>          \_/

## 分析
深度优先或广度优先遍历图即可，用一个字典维护已经被拷贝的节点。

## 代码
### DFS
```python
# Definition for a undirected graph node
class UndirectedGraphNode(object):
    def __init__(self, x):
        self.label = x
        self.neighbors = []


class Solution(object):
    def dfs(self, node, copied):
        if node in copied:
            return copied[node]
        new_node = UndirectedGraphNode(node.label)
        copied[node] = new_node
        for n in node.neighbors:
            new_node.neighbors.append(self.dfs(n, copied))
        return new_node

    def cloneGraph(self, node):
        """
        :type node: UndirectedGraphNode
        :rtype: UndirectedGraphNode
        """
        d = {}
        if not node:
            return None
        return self.dfs(node, d)
```
