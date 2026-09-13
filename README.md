# Trip Pulse Web

一个为韩国旅行制作的单页行程管理网站，适合在手机和桌面浏览器中使用。

## 页面预览

<p align="center">
  <img src="docs/screenshots/home.png" width="31%" alt="当前行程首页">
  <img src="docs/screenshots/itinerary.png" width="31%" alt="全部行程页面">
  <img src="docs/screenshots/expenses.png" width="31%" alt="重要信息与总开销页面">
</p>

<p align="center">
  当前行程 · 全部行程 · 重要信息与总开销
</p>

## 功能

- 按日期浏览旅行行程与地点信息
- 管理重要信息：新增、修改和删除项目
- 支持“单价 × 3 人”与“直接填写总价”两种计价方式
- 自动汇总旅行总开销
- 内置航班、酒店与 KTX 高铁票信息
- 数据保存在浏览器本地存储中

## 本地运行

这是一个无构建步骤的静态网站。可以直接打开 `index.html`，或启动本地静态服务器：

```bash
python3 -m http.server 8765
```

然后访问 <http://127.0.0.1:8765>。

## 改造成其他国家或日期的旅行计划

项目只有一个核心文件 `index.html`，不需要安装前端框架。推荐先 Fork 本仓库，再按下面的顺序修改：

1. **替换每日行程**：在 `index.html` 中搜索 `const seedDays`，修改每一天的 `date`、`label`、`city`、`summary` 和 `items`。日期使用 `YYYY-MM-DD`，每条行程的格式是 `[时间, 标题, 说明]`。
2. **替换机票、车票与酒店**：搜索 `DEFAULT_IMPORTANT_INFOS`，修改或增加项目。`pricing: "unit"` 表示单价乘人数，`pricing: "total"` 表示直接按总价计算。
3. **修改人数**：当前费用计算按 3 人设计。搜索 `price*3`、`单价 × 3 人` 和 `3 人旅行`，将数字和页面文字改成实际人数。
4. **修改时区与旅行边界**：搜索 `tripZoneForNow`、`dayIndexNow`，替换 `Asia/Seoul`、`Asia/Shanghai` 以及首尾日期。其他国家请使用标准 IANA 时区名称，例如 `Asia/Tokyo`、`Europe/Paris` 或 `America/New_York`。
5. **替换路线提示**：搜索 `const routeHints`，键名格式是 `上一站|下一站`，值分别是距离和交通建议。不需要路线提示时可以保留空对象。
6. **修改页面文案与视觉素材**：搜索“韩国”“首尔”“釜山”等文字并替换；封面和地图素材也都内嵌在 `index.html` 中，可以换成自己的图片。
7. **清除旧的浏览器数据**：网站会把编辑结果存到 `localStorage`。修改默认数据后，如果页面仍显示旧内容，请清除此站点的本地存储，或更换代码中的存储键 `koreaTripFixedV3` 和 `koreaImportantInfosV2`。

完成后在本地逐页检查“现在、今天、全部、信息、待办、贴士”，确认日期、时区、费用和移动端弹窗都正常，再提交到自己的仓库并部署。

## 部署

可以直接导入 Vercel 等静态网站托管平台，无需额外构建配置。

## 许可证

[MIT](LICENSE)
