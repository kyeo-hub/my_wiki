---
title: "Mermaid 图表"
weight: 1
---

# Mermaid 图表

Docura 主题支持 Mermaid 图表语法。

## 流程图

```mermaid
graph TD
    A[开始] --> B{条件}
    B -->|是 | C[执行 A]
    B -->|否 | D[执行 B]
    C --> E[结束]
    D --> E
```

## 序列图

```mermaid
sequenceDiagram
    participant 用户
    participant 系统
    participant 数据库

    用户->>系统：请求数据
    系统->>数据库：查询
    数据库-->>系统：返回数据
    系统-->>用户：显示结果
```

## 甘特图

```mermaid
gantt
    title 项目计划
    dateFormat  YYYY-MM-DD
    section 阶段 1
    需求分析 :a1, 2024-01-01, 14d
    section 阶段 2
    设计 :after a1, 10d
    开发 :20d
    section 阶段 3
    测试 :15d
```

## 类图

```mermaid
classDiagram
    class Animal {
        +String name
        +eat()
    }
    class Dog {
        +bark()
    }
    class Cat {
        +meow()
    }
    Animal <|-- Dog
    Animal <|-- Cat
```
