

# TikTok Minis Vue Drama Demo
https://bytedance.larkoffice.com/wiki/NjgSwYNSHiiMdxkJHHwcTY1lnCg
https://bytedance.larkoffice.com/wiki/MJ2BwFqSxi4r2SkwHS8cRrlsnVb

基于 Vue 3、TypeScript、Vue Router、Vant、Tailwind CSS 和 TikTok Minis SDK
的短剧示例。业务基础由 `tiktok-minis-drama-demo.zip` 的 React 示例迁移而来。

当前包含：

- 短剧广场、分类和海报列表。
- 沉浸式播放页、上下滑切集、选集面板和基础互动 UI。
- 单 Player 实例复用，正常切集使用 `playNext()`。
- 广场 MANUAL 预加载与播放页 AUTO 前后集预加载。
- Mock API、DTO 适配层和可替换的短剧数据模型。
- WebView 前后台暂停与恢复。

## 启动

```bash
npm install
npm run dev
```

开发服务默认运行在 `http://localhost:8080`：

- 广场：`http://localhost:8080/playlet/square`
- 播放页：`http://localhost:8080/playlet/theater?id=test`

Mock 数据和真实播放标识位于 `src/api/mock-data.ts`。接入后端时，将
`src/api/client.ts` 中的 `MOCK_API_ENABLED` 改为 `false`，并替换
`API_BASE_URL`；服务端字段映射统一放在 `src/api/adapters.ts`。

## 配置 TikTok Client Key

将 `index.html` 中的值设置为 Developer Portal 中应用的 Client Key：

```js
TTMinis.init({
  clientKey: "your_client_key",
})
```

`minis dev` 会静态检查这里的 Client Key，因此不能使用 Vite HTML
环境变量占位符。普通浏览器可验证页面渲染；Minis Player、登录、授权和支付等
客户端能力需要在 TikTok Minis 调试或平台预览环境中验证。

## 本地调试

```bash
npm run debug
```

该命令会用项目当前 Client Key 启动 `minis dev`。播放器构造器来自
`TTMinis.getPlayer()`，播放器适配层位于 `src/plugins/minis-player/`，Vue
生命周期封装位于 `src/composables/useMinisPlayer.ts`。

## 构建网页产物

```bash
npm run build
```

构建产物输出到 `dist`。

## 生成 TikTok Minis 上传包

```bash
npm run build:minis
```

也可以使用当前项目的别名：

```bash
npm run sandbox
```

该命令会：

1. 执行 TypeScript 检查和 Vite 生产构建。
2. 将 `minis.config.json` 写入 `dist`。
3. 校验 SDK 引入顺序和产物体积。
4. 在用户目录的 `__TTMinis__/<client-key>/minis.zip` 生成上传包。

## 上传与发布

1. 登录 TikTok for Developers，进入对应的 Mini Drama 应用。
2. 打开 `Code version`，点击 `Upload code asset`。
3. 选择生成的 `minis.zip`，填写版本备注并点击 `Add asset`。
4. 在 Preview 中扫码真机预览。
5. 完成测试后提交审核，通过后选择 Production 或 Partial rollout 发布。

上传前还需要完成企业验证、行业资质、应用基本信息、隐私政策、服务条款、请求域名白名单，以及平台要求的登录等能力接入。

