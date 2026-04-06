# 知识条目元数据 Schema

所有知识条目文件均以 YAML Front Matter 作为元数据块，放在文件最顶部。

## 必填字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `id` | string | 全局唯一 ID，与注册表一致，如 `code-001` |
| `title` | string | 条目标题 |
| `type` | string | 所属插件类型，如 `code` / `literature` |
| `created` | date | 创建日期，格式 `YYYY-MM-DD` |

## 选填字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `tags` | list[string] | 标签列表，便于检索 |
| `updated` | date | 最后更新日期 |
| `source` | string | 来源链接或引用 |
| `author` | string | 原作者或录入者 |
| `language` | string | 编程语言（code 类型专用） |
| `difficulty` | string | 难度：`beginner` / `intermediate` / `advanced` |
| `status` | string | 条目状态：`draft` / `review` / `stable` |

## 示例

```yaml
---
id: code-001
title: 二叉树中序遍历（递归 & 迭代）
type: code
created: 2026-04-06
tags: [算法, 树, Python]
language: Python
difficulty: intermediate
status: stable
---
```
