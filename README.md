# GitHub 个人主页卡片

一个动态、自动更新的 GitHub 个人主页 SVG 卡片，展示你的项目、编程语言、贡献统计等信息。

**[English](README_EN.md)**

<div align="center">
  <img src="https://raw.githubusercontent.com/2982136527/2982136527/main/profile-card.svg" width="960" alt="Profile Card" />
</div>

## 功能特性

- **编程语言星轨** — 自动检测你使用最多的 12 种编程语言，以行星轨道方式环绕太阳展示
- **项目列表** — 展示所有仓库，包含描述、语言和最后更新日期
- **活动面板** — 显示贡献数、仓库数、关注者和连续贡献进度
- **贡献蛇形图** — 动画蛇形路径展示你的贡献日历
- **自动更新** — 每 6 小时通过 GitHub Actions 自动刷新

## 快速开始

### 方式一：Fork 本仓库（推荐）

1. 点击右上角 **Fork** 按钮
2. 前往你 fork 后的仓库的 **Actions** 页面
3. 点击 "I understand my workflows, go ahead and enable them" 启用 workflow
4. 点击 **Run workflow** 手动触发一次
5. 等待运行完成，你的 `profile-card.svg` 就生成好了！

> Fork 后会自动使用你的 GitHub 用户名、仓库、语言等数据，无需修改任何代码。

### 方式二：手动创建

1. 创建一个与你的 GitHub 用户名**同名**的仓库
2. 复制 `.github/workflows/update-profile.yml` 和 `hero-banner.svg` 到新仓库
3. 前往 Actions 页面运行 workflow

## 自定义

### 修改配色主题

默认使用粉色/紫色/青色配色。在 workflow 中搜索替换以下颜色：

| 颜色 | 用途 |
|------|------|
| `#FF69B4` | 主色粉色 |
| `#D4A5FF` | 副色紫色 |
| `#00D4FF` | 点缀青色 |
| `#00ff88` | 成功绿色 |
| `#0a0a1a` | 背景色 |

### 修改更新频率

编辑 workflow 中的 `cron` 行：

```yaml
on:
  schedule:
    - cron: "23 */6 * * *"  # 每 6 小时的第 23 分钟
```

### 添加自定义语言图标

编辑 workflow 中的 `LANG_MAP` 对象：

```javascript
'YourLang': { abbr: 'YL', color: '#FF0000', textColor: '#fff' },
```

## 工作原理

1. **GitHub Actions** 按计划运行（每 6 小时）或手动触发
2. 通过 GitHub API 获取你的仓库、语言、贡献和关注者数据
3. 生成包含以下内容的 SVG：
   - 基于你实际语言的动态编程语言星轨
   - 仓库项目列表
   - 真实统计数据面板
   - 贡献日历蛇形图
4. 将更新后的 SVG 提交到仓库

## 常见问题

**Q: 为什么看不到私有仓库？**
A: 需要按上述步骤设置 Personal Access Token (PAT)。

**Q: 可以去掉星轨部分吗？**
A: 可以，删除 workflow 中的 `arsenalSection` 部分并调整高度计算即可。

**Q: SVG 显示的是旧版本？**
A: GitHub 会缓存 SVG 文件。在 README 的图片 URL 后添加 `?v=时间戳`，或等待几分钟。

## 开源协议

MIT — 随便用！
