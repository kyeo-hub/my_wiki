# 部署指南

## 前提条件

1. GitHub 账号
2. 阿里云账号（用于 ESA 部署）

## 第一步：推送代码到 GitHub

```bash
cd /hugo
git push -u origin main
```

## 第二步：配置 GitHub Secrets

在 GitHub 仓库中配置以下 Secrets：

1. 访问 https://github.com/kyeo-hub/my_wiki/settings/secrets/actions
2. 点击 "New repository secret"
3. 添加以下 Secret：

### DEPLOY_KEY（用于推送到外部仓库）

生成 SSH 部署密钥：

```bash
# 本地生成密钥对（不要设置密码）
ssh-keygen -t ed25519 -C "github-actions-deploy" -f ~/.github/deploy_key

# 显示公钥
cat ~/.github/deploy_key.pub
```

将公钥添加到目标仓库的 Deploy Keys：
1. 访问 https://github.com/kyeo-hub/my_wiki/settings/keys
2. 点击 "Add deploy key"
3. 粘贴公钥内容
4. 勾选 "Allow write access"
5. 点击 "Add key"

然后将私钥添加到 Secrets：

```bash
# 显示私钥
cat ~/.github/deploy_key
```

将私钥内容粘贴到 GitHub Secret，名称为 `DEPLOY_KEY`。

## 第三步：配置阿里云 ESA

### 3.1 创建 ESA 项目

1. 登录 [阿里云控制台](https://homenew.console.aliyun.com/)
2. 访问 [边缘安全加速 ESA](https://esa.console.aliyun.com/)
3. 创建新项目

### 3.2 配置 Git 自动部署

1. 在 ESA 项目页面，找到 "部署" 或 "CI/CD" 选项
2. 选择 "GitHub" 作为代码源
3. 授权访问 GitHub
4. 选择仓库：`kyeo-hub/my_wiki`
5. 选择分支：`gh-pages`
6. 配置构建设置：
   - 构建命令：`hugo --minify --gc`（如果需要 ESA 构建）
   - 发布目录：`.` 或 `/`（因为 gh-pages 分支已经是构建后的静态文件）

### 3.3 配置域名（可选）

如果需要自定义域名：
1. 在 ESA 项目设置中添加域名
2. 配置 DNS CNAME 记录指向 ESA 提供的地址

## 第四步：验证部署

### GitHub Actions

1. 访问 https://github.com/kyeo-hub/my_wiki/actions
2. 查看 "Deploy to Git Repository" 工作流
3. 确保所有步骤都显示绿色 ✓

### 访问网站

- **GitHub Pages**: `https://kyeo-hub.github.io/my_wiki/`
- **阿里云 ESA**: 部署完成后访问 ESA 提供的域名或你的自定义域名

## 本地开发

```bash
# 启动开发服务器
/usr/local/bin/hugo server -D --bind 0.0.0.0

# 访问 http://localhost:1313
```

## 添加新内容

### 创建新页面

```bash
# 使用 Hugo 命令
hugo new content 入门指南/新页面.md

# 或手动创建 markdown 文件
```

### 页面 Front Matter

```markdown
+++
title = "页面标题"
weight = 1      # 排序权重，数字越小越靠前
date = 2024-01-01
+++

页面内容...
```

### 使用 Shortcodes

Docdock 主题提供了一些有用的 shortcodes：

```markdown
{{% notice note %}}
这是一个注释框
{{% /notice %}}

{{% notice tip %}}
这是一个提示框
{{% /notice %}}

{{% notice info %}}
这是一个信息框
{{% /notice %}}

{{% notice warning %}}
这是一个警告框
{{% /notice %}}
```

## 故障排除

### GitHub Actions 失败

1. 检查 Secrets 是否正确配置
2. 查看 Actions 日志了解具体错误
3. 确保 deploy key 有写权限

### ESA 部署失败

1. 确认 gh-pages 分支有内容
2. 检查 ESA 构建配置
3. 查看 ESA 部署日志

### 本地构建问题

```bash
# 清理缓存重新构建
hugo --cleanDestinationDir --gc

# 查看详细日志
hugo --logLevel debug
```

## 主题定制

修改 `hugo.toml` 配置主题：

```toml
[params]
  themeVariant = "blue"  # blue, green, red, orange
  disableSearch = false
  showVisitedLinks = true
```

更多配置参考：[Docdock 文档](https://github.com/vjeantet/hugo-theme-docdock)
