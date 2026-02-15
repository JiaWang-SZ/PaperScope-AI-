# GitHub Pages 部署设置指南

## 重要提示

本仓库已经完成了代码层面的配置，但还需要在 GitHub 仓库设置中完成以下配置步骤才能使部署生效。

## 必需的仓库设置步骤

### 1. 启用 GitHub Pages

1. 进入仓库页面：https://github.com/JiaWang-SZ/PaperScope-AI-
2. 点击 **Settings**（设置）标签
3. 在左侧菜单中找到 **Pages**
4. 在 **Source** (来源) 下拉菜单中选择：**GitHub Actions**
5. 保存设置

**重要：** 不要选择 "Deploy from a branch"，必须选择 "GitHub Actions"！

### 2. 配置 Actions 权限

1. 在仓库的 Settings 页面
2. 在左侧菜单中找到 **Actions** → **General**
3. 滚动到 **Workflow permissions** 部分
4. 选择：**Read and write permissions**
5. 勾选：**Allow GitHub Actions to create and approve pull requests**（可选）
6. 点击 **Save** 保存

### 3. 合并 Pull Request 并触发部署

1. 将当前的 Pull Request 合并到 `main` 分支
2. 合并后会自动触发 "Deploy to GitHub Pages" 工作流
3. 等待几分钟让部署完成

### 4. 验证部署

部署完成后，访问：https://jiawang-sz.github.io/LabPage/

**注意：** 首次部署可能需要 5-10 分钟才能生效。

## 检查部署状态

### 查看 Actions 运行状态

1. 进入仓库的 **Actions** 标签页
2. 查看 "Deploy to GitHub Pages" 工作流
3. 确认运行状态为绿色勾号（成功）

### 查看 Pages 部署状态

1. 进入 **Settings** → **Pages**
2. 查看 "Your site is live at" 消息
3. 点击链接验证网站是否正常

## 后续更新

设置完成后，每次推送到 `main` 分支都会自动触发部署：

```bash
git add .
git commit -m "更新说明"
git push origin main
```

几分钟后，更新会自动出现在网站上。

## 故障排查

如果遇到问题，请参考：
- [GITHUB_PAGES_DEPLOYMENT.md](./GITHUB_PAGES_DEPLOYMENT.md) - 详细的部署文档
- GitHub Actions 日志 - 查看具体错误信息
- GitHub Pages 设置页面 - 确认配置是否正确

## 已完成的代码更改

✅ 创建了 `.github/workflows/deploy-pages.yml` 工作流
✅ 配置了 `vite.config.ts` 的 base path 为 `/LabPage/`
✅ 添加了完整的文档和说明
✅ 测试了本地构建流程

现在只需要完成上述的仓库设置步骤即可！
