# T9 线路优选入口

这是一个可直接部署到 GitHub Pages 的纯静态页面，无需构建工具或外部 CDN。

## 当前配置

- 品牌：T9 国际
- 测速线路：`tian901.com`、`tian902.com`、`tian903.com`、`tian905.com`、`tian906.com`、`tian907.com`、`tian908.com`、`tian909.com`
- 备用网址：`https://tian909.com`
- 永久收藏地址：部署后自动显示当前 GitHub Pages URL
- 测速资源：各线路根目录的 `/t9-logo.png`
- 离线支持：首次在线打开后缓存首页、Logo 和 PWA 图标，后续优先显示本地副本并后台更新

## 离线与 PWA

- 页面通过 `sw.js` 注册 Service Worker，仅缓存当前 GitHub Pages 域名下的静态资源。
- 用户必须至少成功访问一次，浏览器完成 Service Worker 安装后，离线缓存才会生效。
- iOS Safari 可通过“分享 → 添加到主屏幕”保存；Android 浏览器可使用“安装应用/添加到主屏幕”。
- 浏览器清除网站数据、无痕模式或首次访问时发布域名已不可达，均无法使用缓存。
- 外部备用域名不会被跨域缓存；离线时页面可显示，但外部线路仍需要网络才能打开。

## 添加更多测速线路

在 `index.html` 的 `#rotation-list` 中复制下面这一行，并替换域名：

```html
<a class="line" data-probe href="https://example.com" target="_blank" rel="noopener"><span class="rank">·</span><span class="host">example.com</span><span class="status testing">测速中</span></a>
```

各测速域名需要能通过 HTTPS 访问 `/t9-logo.png`。页面会并行请求该图片三次，以加载耗时的中位数排序。测速只能反映浏览器到静态资源的访问情况，不代表整站所有接口速度。

## GitHub Pages

1. 将仓库设为公开仓库。
2. 打开仓库 **Settings → Pages**。
3. 在 **Build and deployment** 中选择 **Deploy from a branch**。
4. 选择 `main` 分支和 `/ (root)`，保存。
5. 等待 GitHub Actions/Pages 完成部署。

## 本地预览

```bash
python3 -m http.server 4175
```

然后访问 `http://localhost:4175/`。

