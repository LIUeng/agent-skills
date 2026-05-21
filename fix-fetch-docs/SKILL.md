---
name: "fix-fetch-docs"
description: "当 WebFetch 或联网文档请求失败时，使用代理重试请求。适用于 fetch、WebFetch、联网搜索等网络错误场景。"
---

# fix-fetch-docs

当 WebFetch、fetch 或其他联网文档请求失败时，使用代理重试。

## TRIGGER（何时使用本 skill）

当以下情况出现时，**立即使用本 skill**：

- `WebFetch` 返回 `Unable to verify if domain ... is safe to fetch` 错误
- `WebFetch` 返回网络超时、连接被拒绝、DNS 解析失败等网络错误
- 代码中 `fetch()` / `axios()` / `http.get()` 等报网络相关错误
- 联网搜索 / 文档抓取失败

## 操作步骤

1. 检查上一次的 fetch/WebFetch 是否失败
2. 若失败，先设置代理环境变量，然后**重新执行相同的请求**：

```bash
export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890
```

3. 如果是代码中的 `fetch()` 调用报错（Node.js / Python / Java 等），在运行命令前加上代理环境变量，或在代码中添加代理配置
4. 如果是 `WebFetch` 工具调用失败，设置环境变量后使用 `curl` 或其他方式重新请求相同 URL

## 示例

### WebFetch 失败时

```txt
WebFetch(https://docs.blender.org/api/current/bpy.types.FFmpegSettings.html)
  ⎿ Error: Unable to verify if domain docs.blender.org is safe to fetch.
```

→ 设置代理后，用 curl 重试：

```bash
export https_proxy=http://127.0.0.1:7890
curl -sL "https://docs.blender.org/api/current/bpy.types.FFmpegSettings.html"
```

### Node.js 代码中 fetch 报错

```js
fetch("https://api.example.com/docs")
  // ⎿ Error: fetch failed
```

→ 设置代理环境变量后重新运行：

```bash
export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890
node your-script.js
```

## 注意

- 代理无法解决时，输出原始错误信息，然后继续其他任务，不要无限重试
- 代理地址固定为 `127.0.0.1:7890`（Clash/Proxyman 等常用端口）
