# 快速设置指南

本指南帮助您快速设置 GitHub Pages 以正确显示网站。

## ⚠️ 关键配置步骤

### 步骤 1: 确保 GitHub Pages Source 配置正确

这是最重要的一步！如果配置错误，网站将无法正常显示。

1. 访问仓库设置页面:
   ```
   https://github.com/sigrust/sigrust.github.io/settings/pages
   ```

2. 在 **Source** 部分:
   - **正确配置**: 选择 **"GitHub Actions"** ✅
   - **错误配置**: 选择 "Deploy from a branch" ❌

3. 如果当前是 "Deploy from a branch"，请点击下拉菜单并选择 **"GitHub Actions"**

4. 保存配置（如果有保存按钮的话）

### 步骤 2: 配置 GitHub Actions 权限

1. 访问 Actions 设置页面:
   ```
   https://github.com/sigrust/sigrust.github.io/settings/actions
   ```

2. 在 **Workflow permissions** 部分:
   - 选择 **"Read and write permissions"** ✅
   - 勾选 **"Allow GitHub Actions to create and approve pull requests"**

3. 点击 **Save** 保存

### 步骤 3: 触发部署

如果您刚刚完成配置，可以通过以下方式触发部署:

#### 方法 1: 推送新的提交（推荐）

```bash
# 在本地仓库中进行任意小的更改
echo "# Setup complete" >> .deployment-trigger
git add .deployment-trigger
git commit -m "Trigger initial deployment"
git push origin main  # 或 master
```

#### 方法 2: 手动触发工作流

1. 访问 Actions 页面: `https://github.com/sigrust/sigrust.github.io/actions`
2. 选择 **ci** 工作流
3. 点击 **Run workflow** 按钮
4. 选择分支（main 或 master）
5. 点击 **Run workflow** 确认

### 步骤 4: 验证部署

1. **监控工作流运行**:
   - 访问 `https://github.com/sigrust/sigrust.github.io/actions`
   - 等待最新的工作流运行完成（显示绿色✅）
   - 通常需要 1-3 分钟

2. **访问网站**:
   - 访问 `https://sigrust.github.io/`
   - 应该看到完整的 Rust 学习资源网站
   - 如果看到 404 或仓库名，请等待 1-2 分钟后刷新

3. **清除缓存**（如果需要）:
   - 按 `Ctrl+Shift+R` (Windows/Linux) 或 `Cmd+Shift+R` (Mac)
   - 或使用浏览器的无痕/隐私模式

## ✓ 验证清单

完成设置后，确认以下所有项目:

- [ ] GitHub Pages Source 设置为 "GitHub Actions"
- [ ] Workflow permissions 设置为 "Read and write permissions"
- [ ] 推送了代码到 main/master 分支
- [ ] GitHub Actions 工作流运行成功（绿色✅）
- [ ] 网站 https://sigrust.github.io/ 可以正常访问
- [ ] 网站显示完整内容和样式

## 🔧 遇到问题？

如果网站仍未正常显示，请参阅:

- [TROUBLESHOOTING.md](TROUBLESHOOTING.md) - 详细的故障排除指南
- [DEPLOYMENT.md](DEPLOYMENT.md) - 完整的部署文档
- [VERIFICATION.md](VERIFICATION.md) - 详细的验证清单

## 📝 后续维护

设置完成后:

1. **添加内容**: 编辑 `docs/` 目录中的 Markdown 文件
2. **提交更改**: 
   ```bash
   git add docs/
   git commit -m "Update content"
   git push
   ```
3. **自动部署**: 推送后，GitHub Actions 会自动构建和部署
4. **查看更新**: 1-2 分钟后访问网站查看更新

## 🎉 完成!

设置完成后，您的 GitHub Pages 网站应该能够正常显示了！

每次推送到 main/master 分支时，网站会自动更新。
