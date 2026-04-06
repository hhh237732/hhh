# 文献知识插件

用于存储**论文阅读笔记、书籍摘要、技术报告、博客精读**等文献类知识。

## 知识条目格式

在 [core/schema.md](../../core/schema.md) 基础上，文献插件推荐额外填写：

```yaml
---
id: lit-001
title: 条目标题
type: literature
created: YYYY-MM-DD
tags: []
source: "https://arxiv.org/..."  # 原文链接
author: "Author et al."          # 原文作者
status: stable                   # draft / review / stable
---
```

## 条目文件结构

```markdown
# 标题

## 基本信息
（作者、发表年份、来源）

## 核心贡献
（论文/书籍的主要创新点或观点）

## 方法/内容摘要
（主要内容概述）

## 关键结论
（结论与实验结果）

## 个人笔记
（读后思考、疑问、与其他工作的联系）

## 参考资料
（引用、相关链接）
```

## 新增条目步骤

1. 在 `knowledge/literature/` 下新建 `<id>-<slug>.md` 文件
2. 填写 Front Matter 元数据
3. 按上方结构编写笔记内容
4. 在本文件 [index.md](index.md) 追加一行索引
5. 在 [core/registry.md](../../core/registry.md) 追加一行注册记录
