---
id: code-001
title: 二叉树中序遍历（递归 & 迭代）
type: code
created: 2026-04-06
tags: [算法, 树, Python]
language: Python
difficulty: intermediate
status: stable
source: "https://leetcode.cn/problems/binary-tree-inorder-traversal/"
---

# 二叉树中序遍历（递归 & 迭代）

## 问题描述

给定一棵二叉树的根节点 `root`，按照**中序遍历**（左 → 根 → 右）返回所有节点的值。

## 核心思路

- **递归**：天然契合树的递归定义，代码简洁。
- **迭代**：使用显式栈模拟系统调用栈，避免递归深度限制，适合工程场景。

## 代码实现

```python
from typing import Optional, List

class TreeNode:
    def __init__(self, val: int = 0,
                 left: "Optional[TreeNode]" = None,
                 right: "Optional[TreeNode]" = None):
        self.val = val
        self.left = left
        self.right = right


# ── 递归版本 ──────────────────────────────────────────
def inorder_recursive(root: Optional[TreeNode]) -> List[int]:
    result: List[int] = []

    def dfs(node: Optional[TreeNode]) -> None:
        if node is None:
            return
        dfs(node.left)
        result.append(node.val)
        dfs(node.right)

    dfs(root)
    return result


# ── 迭代版本 ──────────────────────────────────────────
def inorder_iterative(root: Optional[TreeNode]) -> List[int]:
    result: List[int] = []
    stack: List[TreeNode] = []
    current = root

    while current is not None or stack:
        # 一路向左，将沿途节点压栈
        while current is not None:
            stack.append(current)
            current = current.left
        # 弹出栈顶节点，访问，再转向右子树
        current = stack.pop()
        result.append(current.val)
        current = current.right

    return result
```

## 复杂度分析

| | 时间复杂度 | 空间复杂度 |
|---|---|---|
| 递归 | O(n) | O(h)，h 为树高，最坏 O(n) |
| 迭代 | O(n) | O(h)，最坏 O(n) |

## 参考资料

- [LeetCode 94. 二叉树的中序遍历](https://leetcode.cn/problems/binary-tree-inorder-traversal/)
