API 規格書
===

文件版本修正紀錄表
---
| 版號 | 編號 | 日期 | 修改者 | 項目 | 內容 |
| :-- | :-- | :-- | :-- | :-- | :--|
| v1.0  | 1 | 2026/5/24 | Barry | 新增 | add login|


---


01-v1.0 · 登入 API  
---

### 使用對象
- 頁面上的 login

### 規格
- API：`api/login`
- HTTP Method：POST
- 呼叫參數

| 參數名稱        | 必填 | 資料類型 | 說明 |
| :-------------- | :--: | :------ | :--- |
| StudentNumber   | V    | String  | 帳號，也是學生的學號 |
| StudentPassword | V    | String  | 密碼 |

註:兩個欄位皆為必填

- 範例
    ```
    {
        "StudentNumber":"111703888",
        "StudentPassword":"test01"
    }
    ```  

- 回傳參數

| 參數名稱 | 類型 | 說明 | 範例 |
| :-- | :-- | :-- | :-- |
| StatusCode  | Int | API執行狀態代碼 | 200 |
| Message  | String | API執行狀態說明 | login success |
| Data | List<object> | 回傳資料以及參數 | "StudentNumber":"111703888" |

- 範例
    ```
    {
        "StatusCode":200,
        "Message":"login success",
        "Data": {
            "StudentNumber":"111703888"
        }
    }
    ```

- 狀態說明

| 狀態碼 | 狀態描述 |
| :----- | :------ |
| 200    | 登入成功 |
| 400    | 參數錯誤（缺少帳號或密碼） |
| 401    | 帳號或密碼錯誤 |
| 500    | 伺服器錯誤 |