# Tests-testcase
postman的測試案例透過寫在集合或單一api的test裡，透過編寫各種案例來針對api回應後的結果進行確認。

postman的測試有兩種寫法
* 舊的api寫法
```javascript 
tests[..Test description] = ...Assert; 
//[]內撰寫testcase結果需展示的描述
```
* 類似javescript的寫法
```javascript 
pm.test(...Test description, ...Assert);
//()內撰寫testcase結果需展示的描述
```

## 測試api正確回應
### status code 回應代碼
* code 符合設定值
```javascript
tests["status code is 200"] = responseCode.code === 200;
//設定code值，確認api正確回應200
```
### responseTime 回應時間
* responseTime 符合設定值
```javascript
tests["Response time is less than 200ms"] = responseTime < 200;
//設定毫秒值，確認api回應時間符合所設定的趨勢與數值
```
### responseJson 回應結果測試-絕對結果測試
* 需要測試response是否有回應特定項目對應的value、有則pass、無則failed。
```javascript
const responseJson = pm.response.json()
const ID=responseJson.result.ID
//進行宣告我想要這次的測試叫做ID、並是要搜尋response中的result底下的ID，故寫成".result.ID"，依照資料結構層級撰寫。
pm.test("ID is 33636", function (){pm.expect(ID).to.eql("33636")}); 
//""中輸入測試案例要輸出的text、expert()寫入要查找的變數名、後面""寫入要測試得值，值若是相同、此測試案例才會通過。
```
### responseJson 回應結果測試-多結果驗證
* 需要測試變數結果有多種時使用、可以從測試上看到測試結果。缺點是無法讓測試項目用failed呈現。
```javascript
const responseJson = pm.response.json()
const intervalStatus=responseJson.data.intervalStatus
if(intervalStatus==="preparing"){pm.test("preparing")}else if (identity==="draft"){pm.test("draft")}else if (identity==="processing"){pm.test("processing")}else if (identity==="over"){pm.test("over")}else{pm.test("cancel")}
```
這次我們的目標參數名是intervalStatus，位於第一層，預計回傳值共有五種，draft/preparing/processing/over/cancel，這裡直接用else if 處理並顯示test()裡的text。
### 
