
# Pre-request Script
測試前行為、旨在執行這支api之前需要先執行的動作

## 透過api取得auth並代入postman環境參數中(oneclass)：
1. 需有取得權限的api url、並確認paylod格式
2. 需設定環境變數 url/username/password
3. 需確認密碼格式，若為MD5需先宣告加密處理


```javescript
//若api吃的密碼為MD5加密，要先將密碼處理加密後再置入，加上下方的code。
var pw = CryptoJS.MD5("password").toString();

//*先宣告 pw 為要使用的加密密碼，上面密碼處再改寫成 password: pw 即可。
pm.sendRequest({
    url: pm.environment.get("BASE_URL"),
//先在環境變數裡設定一組變數為BASE_URL、放入要取權限的api url，這裡就可以直接取用，未來透過環境變數去管理即可。
    method: "POST",
//設定打api方法
    header: {
        "content-type": "application/json",
      //設定header的content-type
    },
    body: {
        mode: "raw",
        raw: JSON.stringify({
            username: "{{username}}",
            password: "{{password}}" ,
            from: "Nani"
        })
        //塞入打api要給的body、案例格式為 raw。(payload)
        //這裡把帳號密碼也寫在環境參數裡、方便控管。
    }
}, (err, res) => {
    pm.environment.set("token", res.json().jwt);
//先在環境變數裡設定一組變數為token，把拿來回來的第一層的jwt(此案的token放在jwt裡)，寫到環境參數的token裡。
});
```




