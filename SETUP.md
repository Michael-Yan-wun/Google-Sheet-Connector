# Google Sheets Email Connector 設定指南

## 1. Google Cloud 憑證設定

為了讓應用程式讀取您的 Google 試算表，您需要一個服務帳戶 (Service Account)。

1.  前往 [Google Cloud Console](https://console.cloud.google.com/)。
2.  建立一個新專案 (或選擇現有專案)。
3.  啟用 **Google Sheets API**。
    - 搜尋 "Google Sheets API" 並點擊 **啟用 (Enable)**。
4.  建立 **服務帳戶 (Service Account)**。
    - 前往 **IAM 與管理 (IAM & Admin)** > **服務帳戶 (Service Accounts)**。
    - 點擊 **建立服務帳戶 (Create Service Account)**。
    - 輸入名稱 (例如 "sheets-connector")。
    - 點擊 **建立並繼續 (Create and Continue)** -> **完成 (Done)**。
5.  產生金鑰 (Key)。
    - 點擊剛建立的服務帳戶電子郵件。
    - 前往 **金鑰 (Keys)** 分頁。
    - 點擊 **新增金鑰 (Add Key)** > **建立新金鑰 (Create new key)**。
    - 選擇 **JSON** 並點擊 **建立 (Create)**。
    - 檔案將會下載。**請將其重新命名為 `credentials.json`** 並放入專案資料夾：`/Users/yanwunlin/Work/A.Master/code/google-sheets-connector/`。

## 2. 共用試算表

1.  開啟您的 Google 試算表：[連結](https://docs.google.com/spreadsheets/d/1cngbAvDbb3h7uZwmQZeR4cp3xecRaPgDEbZKA4PMOhk/edit?usp=sharing)
2.  點擊右上角的 **共用 (Share)**。
3.  複製 `credentials.json` 檔案中的 **client_email** (看起來像 `sheets-connector@project-id.iam.gserviceaccount.com`)。
4.  將其貼上到共用對話框中，並給予 **編輯者 (Editor)** 權限。
5.  點擊 **傳送 (Send)** (如果您不想通知，可以取消勾選 "通知使用者")。

## 3. Gmail 應用程式密碼設定

若要透過 Gmail 發送郵件，您需要一組應用程式密碼 (App Password)，而非您的普通密碼。

1.  前往您的 [Google 帳戶安全性](https://myaccount.google.com/security) 頁面。
2.  如果尚未啟用，請啟用 **兩步驟驗證 (2-Step Verification)**。
3.  搜尋 **應用程式密碼 (App Passwords)** (或在 "登入 Google" 下方尋找)。
4.  建立一個新的應用程式密碼 (例如命名為 "Sheets Connector")。
5.  複製產生的 16 字元密碼。

## 4. 環境變數設定

1.  將 `.env.example` 重新命名為 `.env` (或建立一個新的 `.env` 檔案)。
2.  填入以下資訊：

```ini
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=您的16字元應用程式密碼
SPREADSHEET_ID=your_spreadsheet_id_here
GOOGLE_APPLICATION_CREDENTIALS=./credentials.json
PORT=3000
```

## 5. 執行應用程式

1.  在專案資料夾中開啟終端機 (Terminal)。
2.  執行伺服器：
    ```bash
    node server.js
    ```
3.  開啟瀏覽器並前往 `http://localhost:3000`。
4.  您應該會看到試算表中的資料。
5.  點擊 **執行自動回覆 (Execute Auto-Reply)** 來發送郵件並更新試算表。
