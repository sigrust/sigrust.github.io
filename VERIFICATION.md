# GitHub Pages 部署验证清单

本文档提供了一个完整的清单，帮助您验证 GitHub Pages 是否正确配置和部署。

## 前置条件检查

### 1. 仓库文件结构
- [ ] `docs/index.md` 文件存在并包含首页内容
- [ ] `docs/` 目录包含所有导航页面（rust-programming.md, rust-compiler.md, rust-os.md, rust-database.md）
- [ ] `mkdocs.yml` 配置文件存在且配置正确
- [ ] `requirements.txt` 包含所有必需的 Python 依赖
- [ ] `.github/workflows/ci.yml` 工作流文件存在

### 2. 本地构建测试
```bash
# 安装依赖
pip install -r requirements.txt

# 构建网站
mkdocs build

# 验证 site/ 目录生成
ls -la site/
```

- [ ] `mkdocs build` 命令执行成功，无错误
- [ ] `site/` 目录已生成
- [ ] `site/index.html` 文件存在且包含正确内容
- [ ] `site/` 目录包含所有页面子目录

### 3. 本地预览测试（可选）
```bash
# 启动本地开发服务器
mkdocs serve
```

- [ ] 本地服务器启动成功（http://127.0.0.1:8000）
- [ ] 首页显示正确的内容和样式
- [ ] 导航菜单工作正常
- [ ] 所有内部链接可以正常跳转
- [ ] 搜索功能正常工作
- [ ] 深色/浅色主题切换正常

## GitHub 仓库配置

### 4. GitHub Pages 设置
前往仓库设置页面验证：
1. 访问 `https://github.com/sigrust/sigrust.github.io/settings/pages`
2. 检查以下设置：

- [ ] **Source** 设置为 "GitHub Actions"（而非 Deploy from a branch）
- [ ] 显示站点 URL：`https://sigrust.github.io/`

**注意**：如果 Source 设置为分支（如 gh-pages 或 main），请更改为 "GitHub Actions"。

### 5. GitHub Actions 权限
前往仓库 Actions 设置页面验证：
1. 访问 `https://github.com/sigrust/sigrust.github.io/settings/actions`
2. 检查以下设置：

- [ ] **Actions permissions** 允许 "Allow all actions and reusable workflows"
- [ ] **Workflow permissions** 设置为 "Read and write permissions"
- [ ] **Allow GitHub Actions to create and approve pull requests** 已启用（可选）

### 6. GitHub Actions 工作流
查看 Actions 运行状态：
1. 访问 `https://github.com/sigrust/sigrust.github.io/actions`
2. 检查最近的工作流运行：

- [ ] 最近的 `ci` 工作流运行成功（绿色勾选标记）
- [ ] 工作流包含 "Deploy to GitHub Pages" 步骤
- [ ] 部署步骤成功完成

如果工作流失败，点击查看详细日志：
- [ ] 检查 "Setup Python" 步骤是否成功
- [ ] 检查 "Install dependencies" 步骤是否成功
- [ ] 检查 "Build" 步骤是否成功
- [ ] 检查 "Upload artifact" 步骤是否成功
- [ ] 检查 "Deploy to GitHub Pages" 步骤是否成功

## 部署验证

### 7. 网站可访问性
- [ ] 访问 `https://sigrust.github.io/` 可以正常打开
- [ ] 首页显示 "Rust课程和学习资料推荐" 标题
- [ ] 页面显示 Rust 🦀 图标
- [ ] 页面样式正确加载（Rust 主题橙色）
- [ ] 导航栏显示所有页面链接

### 8. 网站功能测试
- [ ] 点击导航链接可以跳转到对应页面
- [ ] 搜索框可以正常使用
- [ ] 深色/浅色主题切换正常工作
- [ ] GitHub 仓库链接正确指向 `https://github.com/sigrust/sigrust.github.io`
- [ ] 自定义 CSS 样式正确应用

### 9. SEO 和元数据
在浏览器中查看页面源代码（右键 -> 查看页面源代码）：
- [ ] `<title>` 标签显示 "Rust学习资源"
- [ ] `<meta name="description">` 包含正确的描述
- [ ] `<meta name="author">` 显示 "Rust SIG"
- [ ] `<link rel="canonical">` 指向正确的 URL

## 常见问题排查

### 问题 1: 页面显示 404 错误
**可能原因**：
- GitHub Pages Source 未设置为 "GitHub Actions"
- 工作流部署失败

**解决方法**：
1. 检查 GitHub Pages 设置（步骤 4）
2. 查看 Actions 工作流日志（步骤 6）
3. 确认 `site/` 目录在本地构建成功（步骤 2）

### 问题 2: 页面显示但样式不正确
**可能原因**：
- CSS 文件路径错误
- 自定义样式文件未正确部署

**解决方法**：
1. 检查 `docs/stylesheets/extra.css` 文件存在
2. 验证 `mkdocs.yml` 中 `extra_css` 配置正确
3. 在浏览器开发者工具中检查 CSS 加载状态

### 问题 3: 工作流构建失败
**可能原因**：
- 依赖版本不兼容
- Python 版本问题
- 文件路径错误

**解决方法**：
1. 查看 Actions 工作流详细日志
2. 在本地运行 `mkdocs build` 重现问题
3. 检查 `requirements.txt` 中的依赖版本

### 问题 4: 更新内容后网站未刷新
**可能原因**：
- 浏览器缓存
- GitHub Pages 部署延迟
- 工作流未触发

**解决方法**：
1. 清除浏览器缓存或使用无痕模式
2. 等待 1-2 分钟让部署完成
3. 检查 Actions 确认工作流已运行

## 验证完成

如果所有上述检查项都已通过 ✅，恭喜！您的 GitHub Pages 网站已正确配置并成功部署。

如果仍有问题，请：
1. 查看 [DEPLOYMENT.md](DEPLOYMENT.md) 获取详细部署说明
2. 检查 GitHub Actions 工作流日志
3. 在本地运行 `mkdocs build` 和 `mkdocs serve` 进行调试
4. 提交 Issue 寻求帮助

## 持续维护

为确保网站持续正常运行：
- [ ] 定期检查 Actions 工作流运行状态
- [ ] 定期更新依赖版本（`requirements.txt`）
- [ ] 监控网站可访问性
- [ ] 及时更新内容并验证部署
