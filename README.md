# My Wiki

个人知识库，使用 Hugo + Docdock 主题构建。

## 本地开发

```bash
# 安装 Hugo (如果未安装)
# macOS
brew install hugo

# Ubuntu/Debian
sudo apt-get install hugo

# 启动开发服务器
hugo server -D
```

访问 http://localhost:1313 预览。

## 部署

### GitHub Actions 自动部署

推送到 `main` 分支会自动触发部署：

1. 构建静态文件到 `public` 目录
2. 部署到 GitHub Pages
3. 同步到外部仓库 `kyeo-hub/my_wiki` 的 `gh-pages` 分支

### 手动部署

```bash
# 构建
hugo --minify

# 预览构建结果
hugo server
```

## 目录结构

```
.
├── content/           # 内容文件
│   ├── _index.md      # 首页
│   ├── 入门指南/
│   ├── 技术文档/
│   └── 项目笔记/
├── themes/            # 主题
├── static/            # 静态资源
├── layouts/           # 自定义布局
├── hugo.toml          # 配置文件
└── .github/
    └── workflows/
        └── deploy.yml # 部署工作流
```

## 添加新内容

```bash
# 创建新页面
hugo new content 入门指南/新页面.md

# 或手动创建 markdown 文件
```

在 markdown 文件开头添加 Front Matter：

```markdown
+++
title = "页面标题"
weight = 1  # 排序权重
+++

内容正文...
```

## 主题

使用 [Docdock](https://github.com/vjeantet/hugo-theme-docdock) 主题，专为文档和知识库设计。

### 特性

- 📱 响应式设计
- 🔍 内置搜索
- 📊 Mermaid 图表支持
- 🌍 多语言支持
- 🎨 多种主题配色

## License

MIT
