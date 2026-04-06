# 代码知识插件

用于存储**代码片段、算法实现、设计模式示例**等与编程直接相关的知识。

## 知识条目格式

在 [core/schema.md](../../core/schema.md) 基础上，代码插件推荐额外填写：

```yaml
---
id: code-001
title: 条目标题
type: code
created: YYYY-MM-DD
tags: []
language: Python       # 编程语言
difficulty: intermediate  # beginner / intermediate / advanced
status: stable         # draft / review / stable
source: ""             # 参考链接（可选）
---
```

## 条目文件结构

```markdown
# 标题

## 问题描述
（描述该代码解决的问题）

## 核心思路
（简要说明算法/设计思路）

## 代码实现
（代码块）

## 复杂度分析
（时间/空间复杂度，可选）

## 参考资料
（链接或引用，可选）
```

## 新增条目步骤

1. 在 `knowledge/code/` 下新建 `<id>-<slug>.md` 文件
2. 填写 Front Matter 元数据
3. 按上方结构编写内容
4. 在本文件 [index.md](index.md) 追加一行索引
5. 在 [core/registry.md](../../core/registry.md) 追加一行注册记录
