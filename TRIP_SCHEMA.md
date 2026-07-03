# TRIP_SCHEMA.md

本文件说明 Travel Plan 读取的行程 JSON 格式。Starter Kit 不解析 Excel、PDF 或邮件；请先让 AI 或人工把资料整理成这里定义的 JSON。

## 文件位置

```text
public/itinerary-index.json
public/trips/<trip-id>/trip.json
public/trips/<trip-id>/trip-meta.json
public/trips/<trip-id>/review-needed.json
```

## itinerary-index.json

`defaultTripId` 决定网页默认打开哪一趟旅行。

## trip.json 顶层结构

```json
{
  "metadata": {},
  "days": [],
  "events": []
}
```

### metadata

| 字段 | 必填 | 用途 |
| --- | --- | --- |
| `schemaVersion` | 是 | 当前用 `1`。 |
| `tripId` | 是 | 与文件夹名一致。 |
| `dateStart` / `dateEnd` | 是 | 行程开始和结束日期，格式 `YYYY-MM-DD`。 |
| `dayCount` | 建议 | 行程天数。 |
| `recordCount` | 建议 | 事项数量。 |

### days[]

每一天控制页面标题、天气、brief 和当天事件顺序。

| 字段 | 必填 | 用途 |
| --- | --- | --- |
| `date` | 是 | 标准日期。 |
| `route` | 是 | 当天标题，例如城市或城市转场。 |
| `eventIds` | 是 | 当天显示哪些事项。 |
| `brief.hotelChanges` | 是 | 当天入住酒店。 |
| `brief.keyTransportEventIds` | 是 | 今日/明日页和每日 brief 的关键交通。 |
| `brief.importantEventIds` | 是 | 重要提醒。 |
| `weatherLocation` | 否 | 有经纬度则显示天气；没有则降级为“暂未配置天气位置”。 |

### events[]

| 字段 | 必填 | 用途 |
| --- | --- | --- |
| `id` | 是 | 全局唯一；不要重复。 |
| `date` | 是 | 所属日期。 |
| `timeStart` / `timeEnd` | 否 | 时间轴显示和排序。 |
| `what` | 是 | 事项标题，也就是“做什么”。 |
| `place` / `address` | 否 | 地点、地址。 |
| `note` | 否 | 原始备注、提醒、票券说明。 |
| `category` | 否 | `hotel`、`transport`、`parking`、`dining`、`reservation`、`alternative`、`attention` 等。 |
| `important` | 否 | 是否重要。 |
| `transportCard` | 否 | 飞机、火车、大巴、轮船等交通卡片。 |
| `mapTargets` | 否 | Google Maps 按钮。 |

### transportCard

只支持单段交通，复杂转机请拆成多条 event。

`kind` 可用：`flight`、`train`、`bus`、`ferry`、`other`。

### mapTargets

```json
[
  {
    "label": "卢浮宫",
    "query": "Musée du Louvre",
    "kind": "place",
    "existingGoogleMapsUrl": ""
  }
]
```

搜索词建议使用当地语言、官方名称、完整地址或经纬度描述。

## review-needed.json

待办完成状态只保存在用户自己的设备 IndexedDB，不会写回 JSON。
