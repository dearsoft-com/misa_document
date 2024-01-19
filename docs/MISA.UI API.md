# MISA 企業雲端服務 API
# 📁 Folder: 會員中心 


## End-point: 登入
### Method: POST
>```
>/postapi/login.php
>```
### Body formdata

|Param|value|Type|
|---|---|---|
|LoginName|epy001|text|
|PIN|epy001|text|


### Response: 200
```json
{
  "ACSToken": "test-token"
}
```

### Response: 200
```json
{
  "_Error": true,
  "Message": "Invalid login name or PIN"
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 檢查登入
### Method: POST
>```
>/postapi/login.check.php
>```
### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "_Error": false,
  "Message": "OK"
}
```

### Response: undefined
```json
{
  "_Error": true,
  "Message": "Invalid access token"
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 發送雙重驗證
### Method: POST
>```
>/postapi/request-2fa.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "_Error": false,
  "Message": "OK"
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 核實雙重驗證
### Method: POST
>```
>/postapi/verify-2fa.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### Body formdata

|Param|value|Type|
|---|---|---|
|Code|245113|text|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "_Error": false,
  "Message": "OK"
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: LINE Notify 狀態
### Method: POST
>```
>/postapi/line-notify-status.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "_Error": false,
  "Message": "OK"
}
```

### Response: 200
```json
{
  "_Error": true,
  "Message": "Not authorized"
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: LINE Notify 交換令牌
### Method: POST
>```
>/postapi/line-notify-auth.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### Body formdata

|Param|value|Type|
|---|---|---|
|Code|wiCQWt4EmGivT80wZmzSpD|text|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "_Error": false,
  "Message": "OK"
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: LINE Notify 撤銷令牌
### Method: POST
>```
>/postapi/line-notify-revoke.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "_Error": false,
  "Message": "OK"
}
```

### Response: 200
```json
{
  "_Error": true,
  "Message": "Not authorized"
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃
# 📁 Folder: 資料頁面 


## End-point: 查詢資料
### Method: POST
>```
>/postapi/:table.select.php
>```
### Body formdata

|Param|value|Type|
|---|---|---|
|$schema|../schema/vendor_ui/member.json#|text|
|limit|10|text|
|offset|0|text|
|All[0][equal][Gender]|male|text|
|All[1][contain][Name]|Doe|text|
|All[2][range][CreateDateTime][0]|2018-01-01|text|
|All[2][range][CreateDateTime][1]|2018-12-31|text|
|Not[0][equal][UserTYPID]|0nomsosgsadksdf14|text|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
    "page": 1,
    "total": 2,
    "datas": [
        {
            "UserID": "usr001",
            "Name": "John Doe",
            "Gender": "male",
            "UserTYPID": "0gsadmksdfos36nos",
            "CreateDateTime": "2018-03-05 10:23:45"
        },
        {
            "UserID": "usr063",
            "Name": "Joseph Doe",
            "Gender": "male",
            "UserTYPID": "0gsadmksdfos36nos",
            "CreateDateTime": "2018-06-11 10:45:23"
        }
    ]
}
```

### Response: 200
```json
{
    "_Error": true,
    "Message": "$schema is required"
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 新增資料
### Method: POST
>```
>/postapi/:table.create.php
>```
### Body formdata

|Param|value|Type|
|---|---|---|
|$schema|../schema/vendor_ui/member.json#|text|
|UserID||text|
|Name|Jane Doe|text|
|Gender|female|text|
|UserTYPID|0nomsosgsadksdf14|text|
|CreateDateTime||text|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
    "UserID": "usr097",
    "Name": "Jane Doe",
    "Gender": "female",
    "UserTYPID": "0nomsosgsadksdf14",
    "CreateDateTime": "2024-01-17 14:16:32"
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 修改資料
### Method: POST
>```
>/postapi/:table.update.php
>```
### Body formdata

|Param|value|Type|
|---|---|---|
|$schema|../schema/vendor_ui/member.json#|text|
|UserID|usr097|text|
|Name|Jane R. Doe|text|
|Gender|female|text|
|UserTYPID|0nomsosgsadksdf14|text|
|CreateDateTime|2024-01-17 14:16:32|text|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
    "UserID": "usr097",
    "Name": "Jane R. Doe",
    "Gender": "female",
    "UserTYPID": "0nomsosgsadksdf14",
    "CreateDateTime": "2024-01-17 14:16:32"
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 刪除資料
### Method: POST
>```
>/postapi/:table.delete.php
>```
### Body formdata

|Param|value|Type|
|---|---|---|
|$schema|../schema/vendor_ui/member.json#|text|
|deletes[]|usr003|text|
|deletes[]|usr079|text|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
[
    "usr003",
    "usr079"
]
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 匯出資料
### Method: POST
>```
>/postapi/:table.export.php
>```
### Body formdata

|Param|value|Type|
|---|---|---|
|$schema|../schema/vendor_ui/member.json#|text|
|limit|10|text|
|offset|0|text|
|Column[]|Name|text|
|Column[]|Gender|text|
|All[0][equal][Gender]|male|text|
|All[1][contain][Name]|Doe|text|
|All[2][range][CreateDateTime][0]|2018-01-01|text|
|All[2][range][CreateDateTime][1]|2018-12-31|text|
|Not[0][equal][UserTYPID]|0nomsosgsadksdf14|text|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
    "page": 1,
    "total": 2,
    "datas": [
        {
            "Name": "John Doe",
            "Gender": "male"
        },
        {
            "Name": "Joseph Doe",
            "Gender": "male"
        }
    ]
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃
# 📁 Folder: 資源管理 


## End-point: 瀏覽圖片
### Method: GET
>```
>banner?offset=0&limit=12&keyword=banner
>```
### Query Params

|Param|value|
|---|---|
|offset|0|
|limit|12|
|keyword|banner|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "total": 20,
  "datas": [
    {
      "FileName": "https://picsum.photos/seed/5v/300",
      "Title": "ipsum do 0 banner",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "AlbumITMID": "cupidatat0",
      "ThumbnailFileName": "https://picsum.photos/seed/5v/300",
      "Size": "300x300"
    },
    {
      "FileName": "https://picsum.photos/seed/5kg/300",
      "Title": "ad consectetur 1 banner",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "AlbumITMID": "incididunt1",
      "ThumbnailFileName": "https://picsum.photos/seed/5kg/300",
      "Size": "300x300"
    },
    {
      "FileName": "https://picsum.photos/seed/4xf/300",
      "Title": "voluptate tempor 2 banner",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "AlbumITMID": "nostrud2",
      "ThumbnailFileName": "https://picsum.photos/seed/4xf/300",
      "Size": "300x300"
    },
    {
      "FileName": "https://picsum.photos/seed/3y0/300",
      "Title": "est adipisicing 3 banner",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "AlbumITMID": "sit3",
      "ThumbnailFileName": "https://picsum.photos/seed/3y0/300",
      "Size": "300x300"
    },
    {
      "FileName": "https://picsum.photos/seed/7ny/300",
      "Title": "id non 4 banner",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "AlbumITMID": "cillum4",
      "ThumbnailFileName": "https://picsum.photos/seed/7ny/300",
      "Size": "300x300"
    },
    {
      "FileName": "https://picsum.photos/seed/16r/300",
      "Title": "excepteur ullamco 5 banner",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "AlbumITMID": "nisi5",
      "ThumbnailFileName": "https://picsum.photos/seed/16r/300",
      "Size": "300x300"
    },
    {
      "FileName": "https://picsum.photos/seed/3rd/300",
      "Title": "veniam sit 6 banner",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "AlbumITMID": "dolore6",
      "ThumbnailFileName": "https://picsum.photos/seed/3rd/300",
      "Size": "300x300"
    },
    {
      "FileName": "https://picsum.photos/seed/2dt/300",
      "Title": "proident officia 7 banner",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "AlbumITMID": "veniam7",
      "ThumbnailFileName": "https://picsum.photos/seed/2dt/300",
      "Size": "300x300"
    },
    {
      "FileName": "https://picsum.photos/seed/7bk/300",
      "Title": "incididunt dolore 8 banner",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "AlbumITMID": "labore8",
      "ThumbnailFileName": "https://picsum.photos/seed/7bk/300",
      "Size": "300x300"
    },
    {
      "FileName": "https://picsum.photos/seed/2e3/300",
      "Title": "labore esse 9 banner",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "AlbumITMID": "dolore9",
      "ThumbnailFileName": "https://picsum.photos/seed/2e3/300",
      "Size": "300x300"
    }
  ]
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 上傳圖片
### Method: POST
>```
>/postapi/richtext-editor/image.upload.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### Body formdata

|Param|value|Type|
|---|---|---|
|upload|/C:/Users/aaron/Downloads/下載 (2).png|file|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "uploaded": true,
  "url": "/uploads/%E4%B8%8B%E8%BC%89%20(2)_1705563614739.png"
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 刪除圖片
### Method: POST
>```
>/postapi/richtext-editor/image.delete.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### Body formdata

|Param|value|Type|
|---|---|---|
|id|aliqua0|text|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
    "deleted": true
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 瀏覽檔案
### Method: GET
>```
>/postapi/richtext-editor/file.browse.php?offset=0&limit=10&keyword=course
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### Query Params

|Param|value|
|---|---|
|offset|0|
|limit|10|
|keyword|course|


### Response: 200
```json
{
  "datas": [
    {
      "FileName": "https://picsum.photos/seed/3pi/300",
      "Title": "esse sint 0 course",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "FileID": "laborum0",
      "Size": "300KB"
    },
    {
      "FileName": "https://picsum.photos/seed/dy/300",
      "Title": "ullamco proident 1 course",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "FileID": "quis1",
      "Size": "300KB"
    },
    {
      "FileName": "https://picsum.photos/seed/14s/300",
      "Title": "irure in 2 course",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "FileID": "non2",
      "Size": "300KB"
    },
    {
      "FileName": "https://picsum.photos/seed/65p/300",
      "Title": "excepteur eiusmod 3 course",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "FileID": "sit3",
      "Size": "300KB"
    },
    {
      "FileName": "https://picsum.photos/seed/4u2/300",
      "Title": "est anim 4 course",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "FileID": "commodo4",
      "Size": "300KB"
    },
    {
      "FileName": "https://picsum.photos/seed/ux/300",
      "Title": "amet fugiat 5 course",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "FileID": "duis5",
      "Size": "300KB"
    },
    {
      "FileName": "https://picsum.photos/seed/2jo/300",
      "Title": "mollit eu 6 course",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "FileID": "aliqua6",
      "Size": "300KB"
    },
    {
      "FileName": "https://picsum.photos/seed/284/300",
      "Title": "pariatur ex 7 course",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "FileID": "deserunt7",
      "Size": "300KB"
    },
    {
      "FileName": "https://picsum.photos/seed/51g/300",
      "Title": "minim aliqua 8 course",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "FileID": "et8",
      "Size": "300KB"
    },
    {
      "FileName": "https://picsum.photos/seed/tg/300",
      "Title": "dolore voluptate 9 course",
      "ModifyDateTime": "2020-01-01 12:00:00",
      "FileID": "ex9",
      "Size": "300KB"
    }
  ],
  "total": 20
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 上傳檔案
### Method: POST
>```
>/postapi/richtext-editor/file.upload.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### Body formdata

|Param|value|Type|
|---|---|---|
|upload|/C:/Users/aaron/Pictures/starry night small.jpg|file|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "uploaded": true,
  "url": "/uploads/starry%20night%20small_1705564344350.jpg"
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 刪除檔案
### Method: POST
>```
>/postapi/richtext-editor/file.delete.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### Body formdata

|Param|value|Type|
|---|---|---|
|id|voluptate0|text|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "deleted": true
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃
# 📁 Folder: 統計資料圖表 


## End-point: 暢銷商品
### Method: POST
>```
>/postapi/statistic/bestseller.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### Body formdata

|Param|value|Type|
|---|---|---|
|from|1674091445701|text|
|to|1705627445701|text|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "datas": [
    {
      "_Label": "Product003",
      "_Value": 876
    },
    {
      "_Label": "Product009",
      "_Value": 823
    },
    {
      "_Label": "Product005",
      "_Value": 686
    },
    {
      "_Label": "Product001",
      "_Value": 676
    },
    {
      "_Label": "Product008",
      "_Value": 661
    },
    {
      "_Label": "Product002",
      "_Value": 570
    },
    {
      "_Label": "Product006",
      "_Value": 429
    },
    {
      "_Label": "Product004",
      "_Value": 385
    },
    {
      "_Label": "Product007",
      "_Value": 187
    },
    {
      "_Label": "Product010",
      "_Value": 111
    }
  ],
  "total": 10,
  "page": 1
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 會員成長
### Method: POST
>```
>/postapi/statistic/member-growth.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### Body formdata

|Param|value|Type|
|---|---|---|
|from|1674091445701|text|
|to|1705627445701|text|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "datas": [
    {
      "_Label": "2023-01-01",
      "_Value": 586
    },
    {
      "_Label": "2023-02-01",
      "_Value": 610
    },
    {
      "_Label": "2023-03-01",
      "_Value": 620
    },
    {
      "_Label": "2023-04-01",
      "_Value": 634
    },
    {
      "_Label": "2023-05-01",
      "_Value": 657
    },
    {
      "_Label": "2023-06-01",
      "_Value": 718
    },
    {
      "_Label": "2023-07-01",
      "_Value": 801
    },
    {
      "_Label": "2023-08-01",
      "_Value": 823
    },
    {
      "_Label": "2023-09-01",
      "_Value": 848
    },
    {
      "_Label": "2023-10-01",
      "_Value": 932
    },
    {
      "_Label": "2023-11-01",
      "_Value": 1030
    },
    {
      "_Label": "2023-12-01",
      "_Value": 1050
    },
    {
      "_Label": "2024-01-01",
      "_Value": 1089
    }
  ],
  "total": 13,
  "page": 1
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 總銷售額
### Method: POST
>```
>/postapi/statistic/total-sales.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### Body formdata

|Param|value|Type|
|---|---|---|
|from|1674091445701|text|
|to|1705627445701|text|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "datas": [
    {
      "_Label": "2023-01-01",
      "_Value": 115432929
    },
    {
      "_Label": "2023-02-01",
      "_Value": 135318125
    },
    {
      "_Label": "2023-03-01",
      "_Value": 117461047
    },
    {
      "_Label": "2023-04-01",
      "_Value": 94041991
    },
    {
      "_Label": "2023-05-01",
      "_Value": 99529595
    },
    {
      "_Label": "2023-06-01",
      "_Value": 128178343
    },
    {
      "_Label": "2023-07-01",
      "_Value": 83563600
    },
    {
      "_Label": "2023-08-01",
      "_Value": 135509220
    },
    {
      "_Label": "2023-09-01",
      "_Value": 104463267
    },
    {
      "_Label": "2023-10-01",
      "_Value": 142556759
    },
    {
      "_Label": "2023-11-01",
      "_Value": 129474945
    },
    {
      "_Label": "2023-12-01",
      "_Value": 145134399
    },
    {
      "_Label": "2024-01-01",
      "_Value": 107286878
    }
  ],
  "total": 13,
  "page": 1
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 商品銷售
### Method: POST
>```
>/postapi/statistic/product-sales.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### Body formdata

|Param|value|Type|
|---|---|---|
|from|1674091445701|text|
|to|1705627445701|text|
|productId|pdt001|text|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "datas": [
    {
      "_Label": "2023-01-01",
      "_Value": 19698
    },
    {
      "_Label": "2023-02-01",
      "_Value": 82121
    },
    {
      "_Label": "2023-03-01",
      "_Value": 14928
    },
    {
      "_Label": "2023-04-01",
      "_Value": 12875
    },
    {
      "_Label": "2023-05-01",
      "_Value": 50204
    },
    {
      "_Label": "2023-06-01",
      "_Value": 34437
    },
    {
      "_Label": "2023-07-01",
      "_Value": 82104
    },
    {
      "_Label": "2023-08-01",
      "_Value": 32526
    },
    {
      "_Label": "2023-09-01",
      "_Value": 74897
    },
    {
      "_Label": "2023-10-01",
      "_Value": 82121
    },
    {
      "_Label": "2023-11-01",
      "_Value": 50789
    },
    {
      "_Label": "2023-12-01",
      "_Value": 98201
    },
    {
      "_Label": "2024-01-01",
      "_Value": 41378
    }
  ],
  "total": 13,
  "page": 1
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 暢銷專櫃
### Method: POST
>```
>/postapi/statistic/bestseller-counter.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### Body formdata

|Param|value|Type|
|---|---|---|
|from|1674091445701|text|
|to|1705627445701|text|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "datas": [
    {
      "_Label": "est reprehenderit",
      "_Value": 96519
    },
    {
      "_Label": "reprehenderit cillum",
      "_Value": 93687
    },
    {
      "_Label": "Lorem minim",
      "_Value": 92362
    },
    {
      "_Label": "tempor incididunt",
      "_Value": 88580
    },
    {
      "_Label": "incididunt sint",
      "_Value": 80508
    },
    {
      "_Label": "sint consequat",
      "_Value": 69936
    },
    {
      "_Label": "non voluptate",
      "_Value": 67684
    },
    {
      "_Label": "amet cillum",
      "_Value": 55743
    },
    {
      "_Label": "sunt incididunt",
      "_Value": 53605
    },
    {
      "_Label": "nisi tempor",
      "_Value": 37109
    },
    {
      "_Label": "commodo aute",
      "_Value": 22574
    },
    {
      "_Label": "laboris ad",
      "_Value": 16874
    },
    {
      "_Label": "esse amet",
      "_Value": 11048
    }
  ],
  "total": 13,
  "page": 1
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 文件瀏覽
### Method: POST
>```
>/postapi/statistic/document-read.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### Body formdata

|Param|value|Type|
|---|---|---|
|from|1674091445701|text|
|to|1705627445701|text|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "datas": [
    {
      "_Label": "aliqua eiusmod",
      "_Value": 87833
    },
    {
      "_Label": "ut nostrud",
      "_Value": 76270
    },
    {
      "_Label": "commodo nostrud",
      "_Value": 74061
    },
    {
      "_Label": "deserunt mollit",
      "_Value": 57928
    },
    {
      "_Label": "veniam ipsum",
      "_Value": 49294
    },
    {
      "_Label": "dolor consequat",
      "_Value": 42047
    },
    {
      "_Label": "sit exercitation",
      "_Value": 29652
    },
    {
      "_Label": "cillum ut",
      "_Value": 27992
    },
    {
      "_Label": "exercitation dolor",
      "_Value": 18261
    },
    {
      "_Label": "ad est",
      "_Value": 17642
    },
    {
      "_Label": "culpa anim",
      "_Value": 13775
    },
    {
      "_Label": "consectetur aute",
      "_Value": 8700
    },
    {
      "_Label": "duis pariatur",
      "_Value": 8075
    }
  ],
  "total": 13,
  "page": 1
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 物料庫存
### Method: POST
>```
>/postapi/statistic/goods-stock.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "datas": [
    {
      "_Label": "ad tempor",
      "_Value": 8880
    },
    {
      "_Label": "do nostrud",
      "_Value": 8190
    },
    {
      "_Label": "ipsum nulla",
      "_Value": 5683
    },
    {
      "_Label": "irure consectetur",
      "_Value": 5414
    },
    {
      "_Label": "excepteur amet",
      "_Value": 5140
    },
    {
      "_Label": "sunt velit",
      "_Value": 2846
    },
    {
      "_Label": "amet esse",
      "_Value": 1917
    },
    {
      "_Label": "labore deserunt",
      "_Value": 1217
    },
    {
      "_Label": "voluptate incididunt",
      "_Value": 811
    },
    {
      "_Label": "laborum in",
      "_Value": 390
    }
  ],
  "total": 10,
  "page": 1
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 課程儲存空間
### Method: POST
>```
>/postapi/statistic/course-storage.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "datas": [
    {
      "_Label": "et Lorem",
      "_Value": 8417
    },
    {
      "_Label": "labore in",
      "_Value": 8043
    },
    {
      "_Label": "dolor laborum",
      "_Value": 6528
    },
    {
      "_Label": "deserunt eiusmod",
      "_Value": 5277
    },
    {
      "_Label": "aliqua amet",
      "_Value": 4561
    },
    {
      "_Label": "commodo mollit",
      "_Value": 4227
    },
    {
      "_Label": "anim pariatur",
      "_Value": 4124
    },
    {
      "_Label": "commodo culpa",
      "_Value": 2459
    },
    {
      "_Label": "non magna",
      "_Value": 765
    },
    {
      "_Label": "magna cupidatat",
      "_Value": 480
    }
  ],
  "total": 10,
  "page": 1
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## End-point: 商品銷售類別
### Method: POST
>```
>/postapi/statistic/sold-by-type.php
>```
### Headers

|Content-Type|Value|
|---|---|
|Authorization|Bearer test-token|


### Body formdata

|Param|value|Type|
|---|---|---|
|from|1674091445701|text|
|to|1705627445701|text|


### 🔑 Authentication bearer

|Param|value|Type|
|---|---|---|
|token|test-token|string|


### Response: 200
```json
{
  "datas": [
    {
      "_Label": "deserunt ea",
      "_Value": 9041
    },
    {
      "_Label": "dolor dolor",
      "_Value": 6022
    },
    {
      "_Label": "laborum est",
      "_Value": 2688
    }
  ],
  "total": 3,
  "page": 1
}
```


⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃
