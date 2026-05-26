# Montik 批量下载器

零后端、单文件的网页小工具,在浏览器里批量保存网页里的视频和原图。

**🔗 在线使用: https://carycheung.github.io/montik-downloader/**

## 功能

- 粘贴多条链接(每行一个),并发解析
- 智能视频变体去重 — 自动选 H.264 + 最高分辨率
- 卡片预览:视频可直接播放并显示时长,图片显示原始尺寸,下载完后显示文件大小
- 批量勾选 / 仅选视频 / 仅选图片 快捷操作
- 全局下载进度浮层(当前文件名 + 百分比 + 成功/失败计数),完成后自动消失
- 直写到指定文件夹(Chrome / Edge / Arc 通过 File System Access API)
- 所有浏览器都支持的 ZIP 打包兜底
- 没有后端、没有埋点、没有数据回传 — 全部逻辑在你的浏览器里跑

## 工作原理

页面通过公共 CORS 代理获取目标网址 HTML,在响应里扫描媒体 URL,按文件 hash 去重,然后通过 File System Access API 或浏览器原生下载流程逐个保存。除了经代理转发的请求外,没有任何数据离开本机。

## 本地使用

直接用浏览器打开 `index.html` 即可。

## 已知限制

- 公开 CORS 代理(codetabs / corsproxy / allorigins)偶尔会限流或宕机,重试一般就行
- 文件大小无法在下载前预知 — CDN 不通过代理暴露 `Content-Length`
- 故事 / 轮播类内容可能只返回首张
- 仅 HLS 流的视频在纯浏览器 JS 里无法保存

如果想长期稳定,可以把 `index.html` 里的代理换成自己的 [Cloudflare Worker](https://developers.cloudflare.com/workers/) — 5 分钟搞定,免费不限量。

## License

MIT
