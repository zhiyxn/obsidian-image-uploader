# Obsidian 图片上传插件

> 基于 [obsidian-image-uploader](https://github.com/Creling/obsidian-image-uploader) 二次开发 增加自定义 BaseUrl 用来适配有些图床只返回相对路径

[English](README_EN.md) | 简体中文

![](https://i.loli.net/2021/07/16/fxWBeLAESNc6tK9.gif)

这个插件可以在粘贴图片时，自动将剪贴板中的图片调整大小（可选）并上传到任意图床。

## 更新日志

-   0.3.3
    -   添加 Base URL 配置支持
-   0.3.2
    -   添加"上传本页所有本地图片"命令
-   0.3.1
    -   修复一些小问题
-   0.3.0
    -   支持 Obsidian 实时预览编辑器

## 快速开始

### 配置说明

1. **Api Endpoint**：图床 API 的接口地址
2. **Upload Header**：上传请求的请求头，使用 **JSON** 格式
3. **Upload Body**：上传请求的请求体，使用 **JSON** 格式。除非你知道自己在做什么，否则不要修改它
4. **Image Url Path**：HTTP 响应中图片 URL 的路径
5. **Base URL**：可选的基础 URL，用于拼接相对路径。如果 API 返回完整的 URL（以 `http` 开头），则留空
6. **Enable Resize**：是否在上传前调整图片大小
7. **Max Width**：宽度超过此值的图片将按原始宽高比调整大小

### 配置示例

#### Imgur

以 Imgur 为例，上传请求如下：

```shell
curl --location --request POST 'https://api.imgur.com/3/image' \
--header 'Authorization: Client-ID {{clientId}}' \
--form 'image="R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"'
```

因此，`Api Endpoint` 应该填写 `https://api.imgur.com/3/image`，`Upload Header` 应该填写 `{"Authorization": "Client-ID {{clientId}}"}`。

上传请求的响应如下：

```json
{
	"data": {
		"id": "orunSTu",
		"title": null,
		"description": null,
		"datetime": 1495556889,
		"type": "image/gif",
		"animated": false,
		"width": 1,
		"height": 1,
		"size": 42,
		"views": 0,
		"bandwidth": 0,
		"vote": null,
		"favorite": false,
		"nsfw": null,
		"section": null,
		"account_url": null,
		"account_id": 0,
		"is_ad": false,
		"in_most_viral": false,
		"tags": [],
		"ad_type": 0,
		"ad_url": "",
		"in_gallery": false,
		"deletehash": "x70po4w7BVvSUzZ",
		"name": "",
		"link": "http://i.imgur.com/orunSTu.gif"
	},
	"success": true,
	"status": 200
}
```

我们需要的是图片 URL `http://i.imgur.com/orunSTu.gif`，所以 `Image Url Path` 应该填写 `data.link`。

#### Lsky-Pro

[Lsky-Pro](https://github.com/lsky-org/lsky-pro) 是一个开源的自托管图床解决方案。

感谢 [@xaya1001](https://github.com/Creling/obsidian-image-uploader/issues/9#issuecomment-1562861494) 提供的配置示例。

```
Api Endpoint：https://img.domain.com/api/v1/upload

Upload Header:
{
  "Authorization": "Bearer xxxx",
  "Accept": "application/json",
  "Content-Type": "multipart/form-data"
}

Upload Body:
{
  "file": "$FILE"
}

Image Url Path: data.links.url
```

## 功能特性

-   自动上传剪贴板中的图片到任意图床
-   支持在上传前调整图片大小
-   支持批量上传当前页面的所有本地图片
-   支持自定义图床 API 配置
-   支持 Obsidian 实时预览编辑器

## 使用方法

### 粘贴上传

1. 在插件设置中配置好图床 API 参数
2. 在编辑器中直接粘贴图片（Ctrl+V 或 Cmd+V）
3. 插件会自动上传图片并插入 Markdown 链接

### 批量上传本地图片

1. 打开命令面板（Ctrl+P 或 Cmd+P）
2. 搜索并执行"Upload All Local Images in This Page"命令
3. 插件会扫描当前页面的所有本地图片并上传到图床
4. 上传成功后自动替换为在线链接

## 致谢

1. [obsidian-imgur-plugin](https://github.com/gavvvr/obsidian-imgur-plugin)
2. [create-obsidian-plugin](https://www.npmjs.com/package/create-obsidian-plugin)
3. [obsidian-image-uploader](https://github.com/Creling/obsidian-image-uploader)

## 许可证

MIT
