# Rust 教育工作组推荐课程

[![CI](https://github.com/sigrust/sigrust.github.io/workflows/ci/badge.svg)](https://github.com/sigrust/sigrust.github.io/actions)

本站由 **Rust语言兴趣小组** 维护，旨在为 Rust 学习者提供高质量的学习资源和课程推荐。

🔗 **访问地址**: [https://sigrust.github.io/](https://sigrust.github.io/)

## 项目说明

本项目使用 [MkDocs](https://www.mkdocs.org/) 和 [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) 主题构建静态网站，通过 GitHub Pages 进行部署。

## 本地开发

### 环境准备

1. 安装 Python 3.x
2. 安装项目依赖：

```bash
pip install -r requirements.txt
```

### 本地预览

启动本地开发服务器：

```bash
mkdocs serve
```

访问 http://127.0.0.1:8000 查看网站效果。

### 构建网站

生成静态网站文件：

```bash
mkdocs build
```

生成的文件将保存在 `site/` 目录中。

## 部署说明

本项目配置了 GitHub Actions 自动部署流程：

1. 当代码推送到 `master` 或 `main` 分支时，CI 工作流会自动触发
2. 工作流会执行 `mkdocs build` 构建静态网站
3. 构建结果会通过 GitHub Actions 直接部署到 GitHub Pages
4. 网站会自动更新

### GitHub Pages 配置要求

确保仓库的 GitHub Pages 配置如下：
- **Source**: GitHub Actions

详细部署说明请参阅 [DEPLOYMENT.md](DEPLOYMENT.md)。

## 文件结构

```
.
├── docs/                    # 文档源文件目录
│   ├── index.md            # 首页
│   ├── rust-programming.md # Rust编程语言
│   ├── rust-compiler.md    # Rust与编译器
│   ├── rust-os.md          # Rust与操作系统
│   ├── rust-database.md    # Rust与数据库
│   ├── images/             # 图片资源
│   └── stylesheets/        # 自定义样式
├── mkdocs.yml              # MkDocs 配置文件
├── requirements.txt        # Python 依赖
├── .github/workflows/      # GitHub Actions 工作流
└── site/                   # 构建输出目录（不提交到仓库）
```

## 贡献指南

欢迎提交 Pull Request 来完善课程推荐内容。在编写文档时，请遵循：

- [Markdown Rules](https://github.com/markdownlint/markdownlint/blob/master/docs/RULES.md)
- [Markdown 简体中文与西文混排要点](https://github.com/selfteaching/markdown-writing-with-mixed-cn-en)

## 许可证

Copyright © 2026 Rust SIG
