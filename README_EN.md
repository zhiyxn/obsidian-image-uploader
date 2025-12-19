# Obsidian Image Uploader

> Based on [obsidian-image-uploader](https://github.com/Creling/obsidian-image-uploader) with secondary development. Added custom BaseUrl to support image hosting services that only return relative paths.

English | [简体中文](README.md)

![](https://i.loli.net/2021/07/16/fxWBeLAESNc6tK9.gif)

This plugin could resize(optional) and upload the image in your clipboard to any image hosting automatically when pasting.

## Changelog

-   0.3.4
    -   update README
-   0.3.3
    -   Add Base URL configuration support
-   0.3.2
    -   Add 'Upload All Local Images in This Page' command
-   0.3.1
    -   Fix some minor problems
-   0.3.0
    -   Support Obsidian Live Preview Editor

## Getting started

### Settings

1. **Api Endpoint**: the Endpoint of the image hosting api
2. **Upload Header**: the header of upload request in **json** format
3. **Upload Body**: the body of upload request in **json** format. Don't change it unless you know what you are doing
4. **Image Url Path**: the path to the image url in http response
5. **Base URL**: Optional base URL for concatenating relative paths. Leave empty if the API returns a complete URL (starting with `http`)
6. **Enable Resize**: whether resizing images before uploading
7. **Max Width**: images that wider than this will be resized by the natural aspect ratio

### Examples

#### Imgur

Take Imgur as an example. The upload request is something like this:

```shell
curl --location --request POST 'https://api.imgur.com/3/image' \
--header 'Authorization: Client-ID {{clientId}}' \
--form 'image="R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"'
```

So, `Api Endpoint` should be `https://api.imgur.com/3/image` and `Upload Header` should be `{"Authorization": "Client-ID {{clientId}}"}`.

The response of the upload request is:

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

All you need is the image url `http://i.imgur.com/orunSTu.gif`, so `Image Url Path` should be `data.link`.

#### Lsky-Pro

[Lsky-Pro](https://github.com/lsky-org/lsky-pro) is a open-sourced and self-hosted image hosting solution.

Thanks to [@xaya1001](https://github.com/Creling/obsidian-image-uploader/issues/9#issuecomment-1562861494) for this example.

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

## Features

-   Automatically upload clipboard images to any image hosting service
-   Support resizing images before uploading
-   Support batch uploading all local images in the current page
-   Support custom image hosting API configuration
-   Support Obsidian Live Preview Editor

## Usage

### Paste Upload

1. Configure the image hosting API parameters in plugin settings
2. Paste images directly in the editor (Ctrl+V or Cmd+V)
3. The plugin will automatically upload the image and insert the Markdown link

### Batch Upload Local Images

1. Open the command palette (Ctrl+P or Cmd+P)
2. Search and execute the "Upload All Local Images in This Page" command
3. The plugin will scan all local images in the current page and upload them to the image hosting service
4. After successful upload, the links will be automatically replaced with online links

## Thanks

1. [obsidian-imgur-plugin](https://github.com/gavvvr/obsidian-imgur-plugin)
2. [create-obsidian-plugin](https://www.npmjs.com/package/create-obsidian-plugin)
3. [obsidian-image-uploader](https://github.com/Creling/obsidian-image-uploader)

## License

MIT
