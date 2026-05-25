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

---

修課紀錄 API
---

### 使用對象
- 主畫面「查看修課紀錄」按鈕點擊後，渲染修課清單頁面

### 規格
- API：`api/student/details`
- HTTP Method：GET
- 呼叫參數

| 參數名稱        | 必填 | 資料類型 | 說明 |
| :-------------- | :--: | :------ | :--- |
| Authorization   | V    | String  | Bearer JWT Token |
| Category | 否    | String  | 篩選類別 (all, HUM, SOC, NAT, INFO, COL, CHI, ENG, PE) |

- 回傳參數

| 參數名稱 | 類型 | 說明 | 範例 |
| :-- | :-- | :-- | :-- |
| StatusCode  | Int | API執行狀態代碼 | 200 |
| Message  | String | API執行狀態說明 | success |
| Data | List<List<object>> | 該類別下的修課清單 | `請看下面範例` |

- 範例
    ```
    {
        "StatusCode": 200,
        "Message": "success",
        "Data": [
            {
                "passed": true,
                "item": {
                    "title": "哲學概論",
                    "sub_category": "HUM",
                    "is_core": true,
                    "credits": 3
                }
            },
            {
                "passed": false,
                "item": {
                    "title": "Python程式設計",
                    "sub_category": "INFO",
                    "is_core": false,
                    "credits": 3
                }
            }
        ]
    }
    ```  

- 狀態說明

| 狀態碼 | 狀態描述 |
| :----- | :------ |
| 200    | 查詢成功 |
| 500    | 伺服器錯誤 |