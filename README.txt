# 餐補小幫手（Android PWA 原型）

## 目前根據文件實作
- POST `https://pos-api-micron.dudooeat.com/reports/employeesDiningRecords`
- Content-Type: `application/x-www-form-urlencoded`
- 參數：`employee_sn`, `start_date`, `end_date`
- 日期格式：`YYYY/MM/DD`；本版只查詢所選單日（start_date 與 end_date 相同）
- 預期 records：`data.records`
- 排除 `deleted` 與非空 `cancel_time`（但保留 `0000-00-00 00:00:00`）

## 重要限制
1. API 文件表示不需登入，僅靠員工編號即可查詢；這不是身分驗證。不要把網站公開給他人，也不要加入任意員工編號的公開查詢功能。
2. 目前尚未取得成功回應 JSON，日期、金額、商店名稱欄位以常見名稱作暫定映射；當日總額可用性需成功回應後驗證。
3. 直接從瀏覽器呼叫 API 可能因 CORS 失敗。若失敗，需部署私人後端代理；不要把任何秘密憑證寫在前端。
4. 「剩餘餐補」目前是依每日上限扣除當日 API amount 的估算，尚未確認 amount 是折扣前或折扣後，也未確認公司額度結轉規則。需依真實規則調整。
5. 目前只有 PWA 前端原型，不是已部署的線上服務。

## 本機預覽
以靜態 HTTP 伺服器提供這個資料夾（PWA 安裝需 HTTPS 或 localhost）。例如：
`python -m http.server 8000`
再以同一台電腦開啟 `http://localhost:8000`。
手機安裝需將檔案部署到 HTTPS 網址，並測試 API CORS。
