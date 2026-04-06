# 插件接入规范

在本知识库中，每一种知识类型对应一个**插件**。插件是 `plugins/<name>/` 目录，须包含以下结构：

```
plugins/<name>/
├── README.md   # 插件说明：用途、知识条目格式、贡献方式
└── index.md    # 本插件下所有条目的索引列表
```

对应的知识条目存放在：

```
knowledge/<name>/
└── <id>-<slug>.md   # 每个条目一个独立文件
```

## README.md 必须包含

1. 插件名称与用途简述
2. 知识条目 Front Matter 示例（可在 [schema.md](schema.md) 基础上添加插件专属字段）
3. 新增条目的步骤说明

## index.md 格式

与 [registry.md](registry.md) 格式一致，但只列出本插件的条目。

## 命名规范

- 条目文件名：`<id>-<slug>.md`，slug 使用小写字母、数字和连字符，如 `code-001-binary-tree-inorder.md`
- ID 前缀与插件名保持一致，如 `code-*`、`lit-*`
