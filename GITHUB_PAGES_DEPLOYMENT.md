# GitHub Pages 部署说明

## 概述

本仓库配置了自动部署到 GitHub Pages 的功能。当代码推送到 `main` 分支时，会自动触发构建和部署流程。

部署地址：https://jiawang-sz.github.io/LabPage/

## 配置要求

### 1. GitHub Pages 设置

在仓库设置中确保以下配置：

1. 进入仓库 Settings → Pages
2. Source (来源) 设置为 **GitHub Actions**
3. 不需要选择分支，因为部署由 Actions 工作流管理

### 2. 工作流权限

确保 GitHub Actions 有正确的权限：

1. 进入 Settings → Actions → General
2. 在 "Workflow permissions" 部分，确保选择了 **Read and write permissions**
3. 勾选 **Allow GitHub Actions to create and approve pull requests**（如果需要）

## 自动部署流程

### 工作流文件

工作流配置在 `.github/workflows/deploy-pages.yml`，包含两个主要任务：

1. **Build**: 构建 Vite 应用
   - 安装依赖 (npm ci)
   - 运行构建命令 (npm run build)
   - 上传构建产物到 GitHub Pages

2. **Deploy**: 部署到 GitHub Pages
   - 使用官方 deploy-pages action
   - 自动发布到 https://jiawang-sz.github.io/LabPage/

### 触发条件

- 推送到 `main` 分支时自动触发
- 可以在 Actions 标签页手动触发 (workflow_dispatch)

## 故障排查

### 1. 检查工作流运行状态

1. 进入仓库的 Actions 标签页
2. 查看 "Deploy to GitHub Pages" 工作流
3. 检查最近的运行记录，确认是否成功

### 2. 常见问题

#### 问题：工作流失败提示权限错误

**解决方案：**
- 检查仓库的 Actions 权限设置（见上文"工作流权限"部分）
- 确认 `GITHUB_TOKEN` 有足够的权限

#### 问题：部署成功但网站显示 404

**可能原因：**
1. GitHub Pages 未启用或设置错误
2. Base path 配置不正确
3. DNS 传播延迟（新站点可能需要几分钟）

**解决方案：**
1. 确认 Settings → Pages 中 Source 设置为 "GitHub Actions"
2. 检查 `vite.config.ts` 中的 `base: '/LabPage/'` 配置是否正确
3. 等待几分钟后重试

#### 问题：网站资源加载失败（404）

**原因：** Base path 配置错误

**解决方案：**
- 确认 `vite.config.ts` 中的 base 配置为 `/LabPage/`
- 如果修改了配置，重新推送代码触发新的部署

#### 问题：构建失败

**解决方案：**
1. 检查 package.json 中的依赖是否正确
2. 本地运行 `npm install` 和 `npm run build` 测试
3. 查看 Actions 日志中的具体错误信息

### 3. 手动验证构建

在本地测试构建：

```bash
# 安装依赖
npm install

# 构建应用
npm run build

# 预览构建结果
npm run preview
```

构建成功后，`dist` 目录应包含：
- `index.html`: 主 HTML 文件
- `assets/`: 包含 JS、CSS 等资源文件

## 更新部署

### 自动更新

只需将代码推送到 `main` 分支：

```bash
git add .
git commit -m "你的提交信息"
git push origin main
```

工作流会自动运行并更新网站。

### 手动触发部署

1. 进入 Actions 标签页
2. 选择 "Deploy to GitHub Pages" 工作流
3. 点击 "Run workflow"
4. 选择 `main` 分支
5. 点击 "Run workflow" 按钮

## 技术细节

### Vite 配置

`vite.config.ts` 包含 GitHub Pages 的关键配置：

```typescript
export default defineConfig({
  base: '/LabPage/',  // 子路径配置，对应 GitHub Pages URL
  build: {
    outDir: 'dist',   // 构建输出目录
    sourcemap: false   // 不生成 source map（可选）
  }
});
```

### 工作流配置要点

```yaml
permissions:
  contents: read    # 读取仓库内容
  pages: write      # 写入 Pages
  id-token: write   # 用于安全部署

concurrency:
  group: "pages"
  cancel-in-progress: false  # 确保部署按顺序执行
```

## 监控和维护

### 检查部署状态

1. **Actions 标签页**: 查看工作流运行历史和日志
2. **Settings → Pages**: 查看当前部署的版本和 URL
3. **访问网站**: https://jiawang-sz.github.io/LabPage/ 确认更新已生效

### 缓存问题

如果更新后网站未显示最新内容：

1. 清除浏览器缓存（Ctrl+F5 或 Cmd+Shift+R）
2. 尝试在无痕/隐私模式下访问
3. 检查 GitHub Pages 部署历史，确认最新版本已部署

## 支持

如果遇到问题：

1. 查看 Actions 工作流日志
2. 检查本文档的故障排查部分
3. 在仓库中创建 Issue 描述问题
