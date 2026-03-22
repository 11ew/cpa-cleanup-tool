# CPA Cleanup Toolbox

纯静态独立工具，用浏览器直接调用 CLIProxyAPI 现有管理接口：

- `GET /v0/management/auth-files`
- `GET /v0/management/auth-files/download`
- `POST /v0/management/api-call`
- `DELETE /v0/management/auth-files`
- `POST /v0/management/auth-files`

## 目标

- 不修改 `cli-proxy-api.exe`
- 不修改 `static/management.html`
- 上游升级时尽量不受影响
- 删除前先写入本地回收站，降低误删风险

## 使用方式

1. 启动你的 CLIProxyAPI，并确保管理接口可访问。
2. 用浏览器打开 `tools/cpa-cleanup/index.html`。
3. 填写 `Management URL` 和 `Management Token`。
4. 先点“扫描候选”。
5. 确认预览无误后，再点“移入回收站并删除”。
6. 如需恢复，在“本地回收站”里点“恢复”。

## 回收站说明

- 删除前，工具会先下载原始 auth JSON。
- 然后把它保存到当前浏览器的 IndexedDB。
- 删除成功后，可通过“恢复”重新上传回管理接口。

## 安全提示

- `Management Token` 只保存在当前页面内存，不自动持久化。
- 回收站里保存的是原始 auth JSON，通常包含敏感凭证。
- 请只在受信任机器、受信任浏览器环境中使用。
- 如果你清空浏览器站点数据、使用隐身模式、或更换浏览器，回收站数据可能丢失。

## 限制

- 这是前端本地执行，不是服务端后台任务。
- 页面关闭、刷新或浏览器崩溃时，当前执行会中断。
- 回收站依赖浏览器 IndexedDB；如果浏览器禁用 IndexedDB，则会禁止删除操作。
