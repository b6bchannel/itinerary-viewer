# PRIVACY_CHECKLIST.md

发布 Starter Kit 或分享真实行程前，请检查这一页。

## Starter Kit 发布前

确认仓库里没有：

- 任何旧私人旅行文件夹
- 真实 `trip.json`、`trip-meta.json`、`review-needed.json`
- 真实酒店、航班、火车、地址、订单号、地图搜索词
- Excel、PDF、截图、聊天记录、日志
- IndexedDB 导出备份
- `.git` 历史中的真实数据
- Cloudflare Team Domain
- Google OAuth Client ID / Client Secret
- GitHub repo URL 或个人邮箱
- `.dev.vars`、token、secret、环境变量

建议搜索：

```text
旧旅行 ID
旧旅行标题
旧项目缓存名
真实城市名
真实酒店名
真实航班号
pages.dev
cloudflare
OAuth
Client Secret
```

## 真实行程部署前

- GitHub repo 建议设为 Private。
- Cloudflare Pages 如果不想公开，请开启 Access。
- 不要把 OAuth Client Secret 写进仓库。
- 不要上传原始 Excel / PDF，除非你确认可以公开。
- 分享链接前，用无痕窗口测试访问权限。

## 为什么不能直接把私人仓库改成 template

因为 Git 历史可能恢复出你删除过的真实行程。Starter Kit 应该使用全新仓库，第一条 commit 只包含脱敏后的文件。
