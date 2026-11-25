# ccok

把 Colab（或任何機器）上的本機服務，開到你電腦的 `localhost`。  
只用 Python 3 標準庫，不用裝套件。

通道與登入由 **ccok.ccc.tc** 提供，一般用戶不必自架 server。

## 風險自負

本工具可在自有機器或 Colab 上使用。若你在 **Google Colab**（或其他雲端 notebook）執行 `gpu`／`auth line` 並對外開隧道，可能不符合該平台的使用條款或資源政策（例如遠端 proxy、以網頁／API 為主使用運算資源等）。

- 後果可能包括：runtime 被中止、資源受限、帳號被限制等  
- 是否合規、後果如何，由**你自己**負責；作者與通道維護者不保證、也不承擔因此產生的任何損失  
- 建議僅供個人實驗；正式服務請用你自己控管的主機，勿依賴 Colab managed runtime  

使用本軟體即表示你了解並接受以上風險。

## 最快：LINE 連線

**Colab**（假設服務聽在本機 80，例如 nginx）：

```bash
git clone --depth 1 https://github.com/DevinY/ccok_client.git
cd ccok_client
chmod +x ccok
./ccok auth line 80
```

打開印出的 Login Page，用 LINE 登入。成功後會顯示**連線碼**（頁面可一鍵複製），Colab 會自動掛上通道。

**你的電腦：**

```bash
./ccok <連線碼> 8088
```

瀏覽器開 http://127.0.0.1:8088/ 。程式要留著，關掉就斷線。

（可選）寫進 `.env`，就不用每次 export：

```bash
cp .env.example .env
```

預設已指向官方通道；`.env` 不要提交。

## Colab 注意

- `%cd` 與 `!指令` 不要寫在同一行  
- 若出現 `Unable to read current working directory`，先 `%cd /content` 再重新 clone  

## 進階：MCP 金鑰（AiCenter）

若你已有 AiCenter MCP 金鑰：

```bash
# .env 內設定 CCOK_TOKEN=aic_mcp_…
./ccok gpu          # Colab，上游預設 127.0.0.1:8188
./ccok 8818         # 本機開埠
```

AiCenter「設定 > ComfyUI 主機」填 `http://ccok:17422`，Token 留空。
