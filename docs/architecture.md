# 架构设计文档

## 设计目标

本知识库的核心设计目标：

1. **可扩展**：新增知识类型不改动已有内容，只需添加新插件目录。
2. **低耦合**：各插件相互独立，条目文件自包含。
3. **易检索**：全局注册表 + 插件索引双层检索，标签辅助过滤。
4. **纯文本**：所有内容均为 Markdown + YAML Front Matter，可直接用 Git 管理、diff 对比、全文搜索。

## 微内核映射

| 微内核概念 | 本知识库对应 |
|-----------|------------|
| Microkernel（内核） | `core/`：registry、schema、plugin-spec |
| External Server（外部服务） | `plugins/<name>/`：各知识类型插件 |
| Application（应用数据） | `knowledge/<name>/`：实际知识条目 |
| Client（客户端） | 贡献者、读者、自动化脚本 |
| IPC（进程间通信） | 统一的 Front Matter 元数据接口 + 注册表 |

## 目录结构

```
hhh/
├── README.md                          # 仓库入口
├── core/                              # 微内核
│   ├── README.md
│   ├── registry.md                    # 全局注册表（所有条目的索引）
│   ├── schema.md                      # 元数据字段规范
│   └── plugin-spec.md                 # 插件接入规范
├── plugins/                           # 插件层
│   ├── code/
│   │   ├── README.md                  # 插件说明与贡献方式
│   │   └── index.md                   # 本插件条目索引
│   └── literature/
│       ├── README.md
│       └── index.md
├── knowledge/                         # 知识数据层
│   ├── code/
│   │   ├── code-001-binary-tree-inorder.md
│   │   └── code-002-lru-cache.md
│   └── literature/
│       ├── lit-001-attention-is-all-you-need.md
│       └── lit-002-microkernel-architecture.md
└── docs/
    └── architecture.md                # 本文件
```

## 数据流

```
贡献者
  │
  ├─ 新建条目文件 → knowledge/<plugin>/<id>-<slug>.md
  ├─ 更新插件索引 → plugins/<plugin>/index.md
  └─ 更新全局注册表 → core/registry.md
```

## 扩展新插件

假设要新增"工具/工程配置"类型的知识：

```bash
mkdir -p plugins/tooling knowledge/tooling
# 创建 plugins/tooling/README.md（参考 plugin-spec.md）
# 创建 plugins/tooling/index.md
# 在 core/registry.md 的表格中添加条目行
```

无需修改核心层任何已有文件。

## 约定

- 所有日期使用 `YYYY-MM-DD` 格式。
- 条目 ID 全局唯一，一旦分配不得更改（可标记 `deprecated`）。
- 删除条目时，保留文件并在 Front Matter 中添加 `status: deprecated`，不从注册表移除。
