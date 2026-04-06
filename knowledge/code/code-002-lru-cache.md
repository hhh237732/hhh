---
id: code-002
title: LRU 缓存实现
type: code
created: 2026-04-06
tags: [数据结构, 缓存, Python]
language: Python
difficulty: intermediate
status: stable
source: "https://leetcode.cn/problems/lru-cache/"
---

# LRU 缓存实现

## 问题描述

实现一个满足 **LRU（最近最少使用）** 淘汰策略的缓存，支持：

- `get(key)` — 返回键对应的值，若不存在返回 `-1`，并将该条目标记为最近使用。
- `put(key, value)` — 插入或更新键值对。若容量已满，先淘汰最久未使用的条目再插入。
- 两个操作的时间复杂度均为 **O(1)**。

## 核心思路

使用**哈希表 + 双向链表**的经典组合：

- **哈希表**：`O(1)` 定位到链表节点。
- **双向链表**：维护访问顺序，头部为最近使用，尾部为最久未使用；增删节点 `O(1)`。

Python 中 `collections.OrderedDict` 已内置此结构，可直接复用。

## 代码实现

```python
from collections import OrderedDict


class LRUCache:
    """利用 OrderedDict 实现 LRU 缓存，get/put 均为 O(1)。"""

    def __init__(self, capacity: int) -> None:
        self.capacity = capacity
        self._cache: OrderedDict[int, int] = OrderedDict()

    def get(self, key: int) -> int:
        if key not in self._cache:
            return -1
        # 移到末尾，标记为最近使用
        self._cache.move_to_end(key)
        return self._cache[key]

    def put(self, key: int, value: int) -> None:
        if key in self._cache:
            self._cache.move_to_end(key)
        self._cache[key] = value
        if len(self._cache) > self.capacity:
            # 淘汰最久未使用（头部）
            self._cache.popitem(last=False)


# ── 不依赖 OrderedDict 的手写版本 ──────────────────────
class _Node:
    __slots__ = ("key", "val", "prev", "next")

    def __init__(self, key: int = 0, val: int = 0) -> None:
        self.key = key
        self.val = val
        self.prev: "_Node | None" = None
        self.next: "_Node | None" = None


class LRUCacheManual:
    """手写双向链表 + 哈希表版本，更清晰地展示底层原理。"""

    def __init__(self, capacity: int) -> None:
        self.capacity = capacity
        self._map: dict[int, _Node] = {}
        # 哑头、哑尾节点，简化边界处理
        self._head = _Node()
        self._tail = _Node()
        self._head.next = self._tail
        self._tail.prev = self._head

    def _remove(self, node: _Node) -> None:
        node.prev.next = node.next  # type: ignore[union-attr]
        node.next.prev = node.prev  # type: ignore[union-attr]

    def _insert_tail(self, node: _Node) -> None:
        prev = self._tail.prev
        prev.next = node           # type: ignore[union-attr]
        node.prev = prev
        node.next = self._tail
        self._tail.prev = node

    def get(self, key: int) -> int:
        if key not in self._map:
            return -1
        node = self._map[key]
        self._remove(node)
        self._insert_tail(node)
        return node.val

    def put(self, key: int, value: int) -> None:
        if key in self._map:
            self._remove(self._map[key])
        node = _Node(key, value)
        self._map[key] = node
        self._insert_tail(node)
        if len(self._map) > self.capacity:
            lru = self._head.next   # type: ignore[assignment]
            self._remove(lru)
            del self._map[lru.key]
```

## 复杂度分析

| 操作 | 时间复杂度 | 空间复杂度 |
|------|-----------|-----------|
| `get` | O(1) | — |
| `put` | O(1) | O(capacity) |

## 参考资料

- [LeetCode 146. LRU 缓存](https://leetcode.cn/problems/lru-cache/)
