# ccok

把 Colab（或任何機器）上的本機服務，開到你電腦的 `localhost`。  
只用 Python 3 標準庫，不用裝套件。

通道與登入由 **ccok.ccc.tc** 提供，一般用戶不必自架 server。

## 最快：LINE 連線

**Colab**（假設服務聽在本機 80，例如 nginx）：

```bash
chmod +x ccok
./ccok auth line 80
```

打開印出的 Login Page，用 LINE 登入。成功後會顯示**連線碼**，Colab 會自動掛上通道。

**你的電腦：**

```bash
./ccok <連線碼> 8088
```

瀏覽器開 http://127.0.0.1:8088/ 。程式要留著，關掉就斷線。

（可選）寫進 `.env`，就不用每次 export：

```bash
cp .env.example .env
```

`.env` 不要提交。

## 進階：MCP 金鑰（AiCenter）

若你已有 AiCenter MCP 金鑰：

```bash
# .env
# CCOK_TOKEN=aic_mcp_…
./ccok gpu          # Colab，上游預設 127.0.0.1:8188
./ccok 8818         # 本機開埠
```

AiCenter「設定 > ComfyUI 主機」填 `http://ccok:17422`，Token 留空。
# ccok_client
# ccok_client
