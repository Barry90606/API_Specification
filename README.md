API 規格書
===

文件版本修正紀錄表
---
| 版號 | 編號 | 日期 | 修改者 | 項目 | 內容 |
| :-- | :-- | :-- | :-- | :-- | :--|
| v1.0  | 1 | 2026/5/24 | Barry | 新增 | add login|
| v1.1  | 2 | 2026/5/25 | Barry | 新增 | add student data|


---


01-v1.0 · 登入 API  
---

### 使用對象
- 頁面上的 login

### 規格
- API：`/api/login`
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
| Message  | String | API執行狀態說明 | success |
| Data | List<object> | 回傳資料以及判斷是哪位學生的參數 | "Token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.xxx.yyy","StudentNumber": "111703888","Name": "王小明" |

- 範例
    ```
    {
        "StatusCode":200,
        "Message":"success",
        "Data": {
            "Token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.xxx.yyy",
            "StudentNumber": "111703888",
            "Name": "王小明"
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

02-v1.1 · 學生基本資料 API  
---

### 使用對象
- 取得登入學生的名字、科系、雙主修、輔修，已拿多少通識學分，以及該類型最多可以拿多少，所有類型的通識學分資訊

### 規格
- API：`/api/student/dashboard`
- HTTP Method：GET
- 呼叫參數

| 參數名稱      | 必填 | 資料類型 | 說明 |
| :-------------| :--: | :------ | :--- |
| Authorization |  V   | String  | Bearer JWT Token |

註1:透過此Token判斷是哪一位學生
註2:只需要使用Token，不需要body

- 回傳參數

| 參數名稱 | 類型 | 說明 | 範例 |
| :-- | :-- | :-- | :-- |
| StatusCode  | Int | API執行狀態代碼 | 200 |
| Message  | String | API執行狀態說明 | success |
| Data | List<List<object>> | 回傳學生資料 | `請看下面範例` |

- 範例
    ```
    {
        "StatusCode":200,
        "Message":"success",
        "Data": {
            "StudentInfo": {
                "Name": "王小明",
                "main_department": "資訊科學學系",
                "secondary_department": Null,
                "sub_main1_department": "數位內容學程",
                "sub_main2_department": Null,
                "Minor": null
            },
            "GeneralEducationGraduationCredits": {
                "GeneralEducationRequiredCredits": 28,
                "GeneralEducationTaken": 18
            },
            "CoreGeneralEducation": {
                "Required":3,
                "Taken": 2
            },
            "humanities":{
                
            }
        }
    }
    ```