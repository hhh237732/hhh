# 全局知识条目注册表

本文件是整个知识库的索引入口。每新增一个知识条目，需在此追加一行记录。

## 格式说明

```
| ID | 标题 | 类型 | 插件 | 路径 | 标签 |
```

- **ID**：唯一标识符，格式 `<plugin-prefix>-<序号>`，如 `code-001`
- **类型**：`code` / `literature` / 其他自定义插件类型
- **路径**：相对仓库根目录的文件路径

---

## 注册表

| ID | 标题 | 类型 | 插件 | 路径 | 标签 |
|----|------|------|------|------|------|
| code-001 | 二叉树中序遍历（递归 & 迭代） | code | code | knowledge/code/code-001-binary-tree-inorder.md | 算法, 树, Python |
| code-002 | LRU 缓存实现 | code | code | knowledge/code/code-002-lru-cache.md | 数据结构, 缓存, Python |
| lit-001 | 《Attention Is All You Need》阅读笔记 | literature | literature | knowledge/literature/lit-001-attention-is-all-you-need.md | NLP, Transformer, 深度学习 |
| lit-002 | 《Microkernel Architecture》概述 | literature | literature | knowledge/literature/lit-002-microkernel-architecture.md | 架构, 微内核, 系统设计 |
