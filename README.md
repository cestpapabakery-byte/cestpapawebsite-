# C'EST PAPA — 國王派線上預購網站

法國爸爸開的烘焙坊 · Galette des Rois 預購站。
目前為「**上線版（尚未串接金流）**」：展示商品、取貨規則、金幣抽獎與門市/條款資訊，供顧客瀏覽與 **ECPay 綠界申請審核** 使用。顧客目前透過 LINE／IG／FB 私訊或親臨門市預訂；**線上刷卡 / LINE Pay 將於 ECPay 開通後加上**。

---

## 檔案
```
cestpapa-store/
├─ index.html   ← 整個網站（單頁）
├─ logo.png     ← 品牌 Logo（首頁、頁首、分享預覽都會用到）
└─ README.md    ← 本說明
```
全部都是靜態檔案，不需要伺服器即可上線。

---

## 上線步驟（Cloudflare Pages，免費）

### 1. 建立帳號（一次性）
1. 到 **github.com** 註冊免費帳號（程式碼放這裡）。
2. 到 **dash.cloudflare.com** 註冊免費帳號。

### 2. 把檔案放上 GitHub（用瀏覽器，不需指令）
1. GitHub → **New repository** → 取名 `cestpapa-store` → Create。
2. 進入該 repo → **Add file → Upload files** → 把 `index.html` 與 `logo.png` 拖進去 → **Commit changes**。

### 3. 用 Cloudflare Pages 部署
1. Cloudflare → **Workers & Pages → Create → Pages → Connect to Git**。
2. 選 `cestpapa-store` repo → **Begin setup**。
3. Framework preset 選 **None**；Build command 留空；Output directory 填 `/`（根目錄）。
4. **Save and Deploy**。約一分鐘後會得到一個網址，例如 `cestpapa-store.pages.dev` → **網站上線！**

### 4. 綁定網域 cestpapabakery.com.tw
1. Cloudflare Pages 專案 → **Custom domains → Set up a custom domain** → 輸入 `cestpapabakery.com.tw`。
2. Cloudflare 會給你 DNS 設定值（CNAME / A 記錄）。
3. 到你**購買網域的管理後台**，把那兩筆 DNS 記錄填上。HTTPS 會自動開通。
   - （若把網域的 Nameserver 轉到 Cloudflare 管理，流程會更簡單，可再討論。）

### 5. 更新網站
之後我只要更新 GitHub 上的檔案，Cloudflare 會**自動重新部署**，你無須操作。

---

## ⚠️ 上線前請填寫的空白處（index.html 內標為「【請填寫】」）
- 公司名稱 / **統一編號**（聯絡我們區）
- **客服電話**（聯絡我們區 + 預訂彈窗）
- 取消訂單需提前幾天（退換貨政策）
- 逾時未取貨處理方式（退換貨政策）

> ECPay 綠界審核信用卡時，通常會檢查網站是否具備：商品與價格、退換貨政策、隱私權政策、服務條款、聯絡方式、公司資訊 —— 本站都已備好，把上面空白填上即可。

---

## 之後的付款整合（ECPay 開通後）
下一階段會加上：
- **後端函式**（Cloudflare Pages Functions）處理 ECPay 全方位金流（信用卡 + LINE Pay + ATM）
- 付款成功後**自動記錄訂單到 Google Sheet** + 通知（LINE / Email）
- 你的 ECPay 金鑰（MerchantID / HashKey / HashIV）會以**環境變數**設定在 Cloudflare，不會寫進程式碼。
