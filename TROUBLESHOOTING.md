# GitHub Pages 故障排除指南

本文档提供了 GitHub Pages 部署问题的排查和解决方案。

## 问题症状: 网站无法显示或显示不正确

### 症状 1: 访问网站时显示 404 错误

**最常见原因**: GitHub Pages Source 配置错误

#### 解决步骤:

1. **检查 GitHub Pages 设置**
   - 访问: `https://github.com/sigrust/sigrust.github.io/settings/pages`
   - 确认 **Source** 设置为 **"GitHub Actions"**
   - 如果显示为 "Deploy from a branch"，需要更改为 "GitHub Actions"

2. **验证工作流运行状态**
   - 访问: `https://github.com/sigrust/sigrust.github.io/actions`
   - 确认最近的 `ci` 工作流运行成功（绿色✅）
   - 如果失败，查看日志了解错误详情

3. **检查工作流权限**
   - 访问: `https://github.com/sigrust/sigrust.github.io/settings/actions`
   - 在 "Workflow permissions" 部分
   - 确保选择了 "Read and write permissions"
   - 确保勾选了 "Allow GitHub Actions to create and approve pull requests"

### 症状 2: 网站显示但样式错误或内容不完整

**可能原因**: 构建问题或缓存问题

#### 解决步骤:

1. **检查构建日志**
   - 访问 Actions 标签页
   - 点击最近的工作流运行
   - 查看 "Build" 步骤的输出
   - 确认没有警告或错误

2. **清除浏览器缓存**
   - 按 `Ctrl+Shift+R` (Windows/Linux) 或 `Cmd+Shift+R` (Mac) 强制刷新
   - 或使用浏览器的无痕/隐私模式访问

3. **等待部署完成**
   - GitHub Pages 部署可能需要 1-2 分钟
   - 确认 "Deploy to GitHub Pages" 步骤已成功完成

### 症状 3: 工作流构建失败

**可能原因**: 依赖问题或配置错误

#### 解决步骤:

1. **查看详细错误日志**
   - 在 Actions 页面点击失败的工作流
   - 展开失败的步骤查看具体错误信息

2. **本地复现问题**
   ```bash
   # 克隆仓库
   git clone https://github.com/sigrust/sigrust.github.io.git
   cd sigrust.github.io
   
   # 安装依赖
   pip install -r requirements.txt
   
   # 尝试构建
   mkdocs build
   ```

3. **常见错误及解决方案**:

   **错误**: `ModuleNotFoundError: No module named 'mkdocs'`
   - **原因**: 依赖未正确安装
   - **解决**: 确保 `requirements.txt` 文件存在且包含所有依赖
   
   **错误**: `Config file 'mkdocs.yml' does not exist`
   - **原因**: 配置文件缺失或路径错误
   - **解决**: 确保 `mkdocs.yml` 文件在仓库根目录
   
   **错误**: `Error reading page 'xxx.md'`
   - **原因**: Markdown 文件有语法错误或不存在
   - **解决**: 检查 `docs/` 目录中的文件，修复语法错误

## 验证清单

使用此清单验证所有配置是否正确:

### GitHub 仓库设置

- [ ] GitHub Pages Source 设置为 "GitHub Actions"
- [ ] Workflow permissions 设置为 "Read and write permissions"
- [ ] Actions 已启用 (Settings → Actions → General)

### 文件和配置

- [ ] `.github/workflows/ci.yml` 文件存在且配置正确
- [ ] `mkdocs.yml` 文件存在且配置正确
- [ ] `requirements.txt` 文件包含所有必需依赖
- [ ] `docs/index.md` 文件存在
- [ ] `docs/` 目录包含所有导航页面

### 构建和部署

- [ ] 本地运行 `mkdocs build` 成功
- [ ] `site/` 目录生成且包含 `index.html`
- [ ] GitHub Actions 工作流运行成功
- [ ] 网站可以通过 https://sigrust.github.io/ 访问

## 快速修复命令

如果一切配置正确但网站仍未显示，尝试以下操作:

```bash
# 1. 确保在主分支
git checkout main  # 或 master

# 2. 创建一个小的更改来触发部署
echo "# Trigger deployment" >> .trigger
git add .trigger
git commit -m "Trigger GitHub Pages deployment"
git push

# 3. 监控 Actions 页面
# 访问 https://github.com/sigrust/sigrust.github.io/actions
# 等待工作流完成
```

## 获取帮助

如果按照上述步骤仍无法解决问题:

1. **查看详细文档**:
   - [DEPLOYMENT.md](DEPLOYMENT.md) - 完整部署指南
   - [VERIFICATION.md](VERIFICATION.md) - 详细验证清单

2. **检查 GitHub 状态**:
   - 访问 [GitHub Status](https://www.githubstatus.com/)
   - 确认 GitHub Pages 服务正常运行

3. **提交 Issue**:
   - 在仓库中创建新 Issue
   - 提供以下信息:
     - 问题描述
     - 错误截图
     - Actions 工作流日志
     - 已尝试的解决方案

## 相关资源

- [GitHub Pages 文档](https://docs.github.com/en/pages)
- [GitHub Actions 文档](https://docs.github.com/en/actions)
- [MkDocs 文档](https://www.mkdocs.org/)
- [Material for MkDocs 文档](https://squidfunk.github.io/mkdocs-material/)
