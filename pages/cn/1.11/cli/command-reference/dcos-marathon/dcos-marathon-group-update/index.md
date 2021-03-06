---
layout: layout.pug
navigationTitle: dcos marathon group update
title: dcos marathon group update
menuWeight: 22
excerpt: 更新 Marathon 组属性

enterprise: false
---


# 说明
`dcos marathon group update` 命令让您更新 Marathon 组属性。

# 使用

```bash
dcos marathon group update <group-id> <properties> <key>=<value> [OPTION]
```

# 选项

| 名称，简写 | 说明 |
|---------|-------------|
| `--force` | 在更新期间禁用 Marathon 中的检查。|
# 位置自变量

| 名称，简写 | 说明 |
|---------|-------------|
| `<group-id>`   |  组ID。 您可以使用以下命令查看组ID列表 `dcos marathon group list` 命令。|
| `<properties>`   | 一个或多个JSON对象属性的列表，以空格分隔。 列表必须格式化为 `<key>=<value>`. 例如, `cpus=2,0 mem=308`。如省略，则从 stdin 上提供的 JSON 对象读取属性。|

# 父命令

| 命令 | 说明 |
|---------|-------------|
| [dcos marathon](/cn/1.11/cli/command-reference/dcos-marathon/) | 将应用程序部署到 DC/OS 并对其进行管理。|

