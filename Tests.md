# Test 測試案例
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


