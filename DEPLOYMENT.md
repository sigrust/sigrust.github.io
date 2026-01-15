# 部署指南

本文档说明如何部署和配置 GitHub Pages 网站。

## 自动部署流程

本项目使用 GitHub Actions 实现自动部署。当代码推送到 `main` 或 `master` 分支时，会自动触发部署流程。

### 工作流程

1. **触发条件**: 推送代码到 `main` 或 `master` 分支
2. **构建步骤**:
   - 检出代码 (fetch-depth: 0，获取完整历史用于 git-revision-date 插件)
   - 设置 Python 3.x 环境
   - 安装依赖: `pip3 install -U -r requirements.txt`
   - 构建网站: `mkdocs build`
   - 上传 Pages 工件: 将 `./site` 目录上传为 GitHub Pages 工件
   - 部署到 GitHub Pages: 使用 `deploy-pages@v4` 直接部署

### 部署目标

- **部署方式**: GitHub Actions 工作流部署
- **构建目录**: `./site`

## GitHub Pages 配置

### 配置步骤

1. 进入仓库的 **Settings** 页面
2. 在左侧菜单选择 **Pages**
3. 在 **Source** 部分配置:
   - **Source**: Deploy from a GitHub Actions workflow
4. 点击 **Save** 保存配置（如需要）

**注意**: 使用 GitHub Actions 工作流部署时，无需手动选择分支，Pages 会自动从工作流部署。

### 验证部署

部署完成后，访问 [https://sigrust.github.io/](https://sigrust.github.io/) 查看网站。

如果网站未正确显示，请检查:

1. **GitHub Pages 配置**: 确认 Source 设置为 `gh-pages` 分支
2. **gh-pages 分支**: 确认该分支存在且包含正确的文件
3. **GitHub Actions**: 检查工作流运行状态，确认无错误

## 手动部署（可选）

如果需要手动部署到 gh-pages 分支（不推荐，推荐使用自动部署），可以在本地执行：

```bash
# 安装依赖
pip install -r requirements.txt

# 部署到 gh-pages 分支
mkdocs gh-deploy
```

**注意**: 
- 手动部署需要配置 Git 凭据并具有推送权限
- 推荐使用自动部署工作流而非手动部署
- 自动部署使用 GitHub Actions 工作流，无需 gh-pages 分支

## 常见问题

### 1. 页面只显示 "sigrust" 或仓库名

**原因**: GitHub Pages 可能未配置为从 GitHub Actions 部署。

**解决方法**: 
- 前往仓库 Settings → Pages
- 确认 Source 设置为 "GitHub Actions"

### 2. 部署后页面未更新

**原因**: GitHub Pages 缓存或部署延迟。

**解决方法**:
- 等待 1-2 分钟让 GitHub Pages 完成部署
- 清除浏览器缓存后重新访问
- 检查 Actions 页面确认工作流成功完成

### 3. 构建失败

**原因**: 依赖版本不兼容或配置错误。

**解决方法**:
- 检查 Actions 日志查看具体错误信息
- 验证 `requirements.txt` 中的依赖版本
- 在本地运行 `mkdocs build` 测试构建

## MkDocs 配置说明

### 关键配置项

```yaml
site_url: https://sigrust.github.io/   # 网站 URL
docs_dir: docs                          # 文档源目录
site_dir: site                          # 构建输出目录
```

### 部署相关配置

MkDocs 的构建和部署流程:
- 构建静态网站到 `site/` 目录
- GitHub Actions 将 `site/` 目录内容上传为 Pages 工件
- 直接部署到 GitHub Pages（无需 Jekyll 处理）

## 相关链接

- [MkDocs 文档](https://www.mkdocs.org/)
- [Material for MkDocs 文档](https://squidfunk.github.io/mkdocs-material/)
- [GitHub Pages 文档](https://docs.github.com/en/pages)
