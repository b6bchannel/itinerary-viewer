# FRIEND_SETUP.md

这份说明写给不懂技术的朋友。照着做即可。

## 1. 从模板创建自己的仓库

1. 打开这个 GitHub Template Repository。
2. 点右上角 `Use this template`。
3. 选择 `Create a new repository`。
4. Repository name 可以写 `my-travel-plan`。
5. 如果行程包含酒店、航班、订单号，请选择 `Private`。
6. 点 `Create repository`。

## 2. 准备自己的行程资料

你可以准备 Excel、PDF、Markdown、邮件文字或聊天记录。不要把密码、证件号、银行卡号发给 AI。

把这些文件一起发给 ChatGPT：

```text
TRIP_SCHEMA.md
你的 Excel / PDF / Markdown 行程资料
```

给 ChatGPT 的 prompt 可以这样写：

```text
请根据 TRIP_SCHEMA.md，把我的旅行资料整理成 Travel Plan PWA 可读取的 JSON。
请输出 4 个完整文件：
1. public/trips/my-trip/trip.json
2. public/trips/my-trip/trip-meta.json
3. public/trips/my-trip/review-needed.json
4. public/itinerary-index.json

要求：
- 不要修改 schema。
- 日期格式用 YYYY-MM-DD。
- 交通、酒店、重要提醒要进入 brief。
- Google Maps query 优先用当地语言、官方名称或完整地址。
- 不确定的内容放入 review-needed.json。
- 不要编造订单号、航班号或酒店地址；不确定就写待确认。
```

## 3. 上传 JSON 到 GitHub

1. 打开你的 GitHub 仓库。
2. 进入 `public/trips/`。
3. 新建文件夹，例如 `my-trip`。
4. 上传 ChatGPT 输出的 `trip.json`、`trip-meta.json`、`review-needed.json`。
5. 回到 `public/`，替换 `itinerary-index.json`。
6. 提交 commit。

## 4. 部署到 Cloudflare Pages

1. 登录 Cloudflare。
2. 打开 Workers & Pages。
3. 点 Create application。
4. 选择 Pages。
5. 连接你的 GitHub 仓库。
6. Build command 留空。
7. Output directory 填：`public`。
8. 点 Deploy。

## 5. 是否开启 Cloudflare Access

如果网站里有真实酒店、航班、订单号，建议开启 Access。

可以选择：不开启、一次性验证码、或 Google 登录。OAuth Client Secret 绝对不要上传 GitHub；它只应该保存在 Cloudflare 或 Google Cloud 后台。

## 6. iPhone 使用

1. 用 Safari 打开 Cloudflare Pages 网址。
2. 点分享按钮。
3. 选择“添加到主屏幕”。
4. 出发前打开一次网页，确保行程被缓存。

## 7. 改错或恢复旧版本

如果上传错了 JSON，在 GitHub 文件页面点 History，找到上一个正确版本，复制旧内容覆盖当前文件，再 commit。

如果手机本机编辑测试乱了，在网页底部使用“重置本机数据”。
