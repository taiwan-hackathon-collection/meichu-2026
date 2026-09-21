# 2026 新竹 X 梅竹黑客松 作品收集

2026 年 9 月 19 日 09:00 至 9 月 20 日 11:00（台灣時間）在清華大學舉行，主辦為清大與陽明交大學生團隊與新竹市政府。企業組（黑客組）由 CloudMosa、羅技、AMD、聚陽實業、NXP（與文曄）、愛德萬測試、Google 七家出題，每家 7 隊，共 49 隊；創客交流組由新竹市政府命題。

這個 repo 只有這一份 README，整理我們在 GitHub 上找到的作品 repo、收集狀況，以及每個專案的簡介。確定為本屆作品的 repo 已 fork 到本組織，命名為 `meichu-2026-{組別}--{原 owner}--{原 repo}`，並打上 `meichu-2026`、`track-*`、`verdict-*`、`team-*` topics。找法與腳本在 [scanner](https://github.com/taiwan-hackathon-collection/scanner)。掃描日期 2026-09-21 至 22。

## 收集狀況

| 組別 | 找到隊數 | 確定 | 很可能 | 存疑 | 已 fork 的 repo |
|---|---:|---:|---:|---:|---:|
| CloudMosa | 8 | 5 | 2 | 1 | 9 |
| 羅技 | 2 | 2 | 0 | 0 | 2 |
| AMD | 7 | 6 | 1 | 0 | 6 |
| 聚陽 | 4 | 4 | 0 | 0 | 5 |
| NXP | 4 | 4 | 0 | 0 | 3 |
| 愛德萬 | 5 | 4 | 1 | 0 | 4 |
| Google | 4 | 4 | 0 | 0 | 8 |
| 組別不明 | 3 | 0 | 1 | 2 | 0 |
| 創客交流組 | 7 | 6 | 0 | 1 | 7 |

- 企業組折算後找到 37 隊（含組別不明與存疑），距 49 隊還缺約 12 隊，缺口主要在羅技（缺 5）、Google（缺 3）、聚陽（缺 3）、NXP（缺 3）、愛德萬（缺 2）。羅技組有保密協定，推測多數隊伍未公開。
- 「確定」指名稱或 README 明講本屆梅竹；「很可能」指使用了該組專屬資源（Cloud Phone、FRDM-i.MX93、Advantest 沙盒、MI300 等）且時間吻合但未提活動；「存疑」指主題或時間吻合但缺乏證據。fork 的 45 個確定 repo 中，milktea7654/2026-meichu 在 fork 前已轉為私有或刪除，未能保存。
- 同一隊常有多個 repo（前後端拆開、隊員副本、fork），下表以隊為單位介紹，副本一併列出。
- 找不到的隊伍多半是 repo 未公開，或 README 完全沒提活動且帳號未填所在地，公開資料無法辨識；若主辦提供作品連結清單，可以直接補齊。

## 專案介紹

每個專案分「概念」與「技術」兩點：概念講它要解決什麼與特別之處，技術講實際的語言、框架、模型、硬體與架構，整理自 README、目錄結構與套件清單；合計約一百到三百字，內容整理自各 repo 的 README 與程式碼，未經團隊本人確認；有錯請開 issue 指正。

### CloudMosa：Cloud Phone 功能機應用

**AgriLink** — [dogbark-MeiChu/dogbark](https://github.com/dogbark-MeiChu/dogbark)（fork：[meichu-2026-cloudmosa--dogbark-MeiChu--dogbark](https://github.com/taiwan-hackathon-collection/meichu-2026-cloudmosa--dogbark-MeiChu--dogbark)；副本 ellatso/dogbark、ellatso/elladogbarktest、Hayamayama/DEMO_Agrilink）
- 概念：讓只有功能機的小農在按鍵手機上看官方批發行情、就近買賣、互助問答並記錄每日農務；TruePrice 算出扣掉運費、佣金與耗損後真正拿到的錢。
- 技術：Node.js 22 加 Express 的後端，PostgreSQL 存資料，PGlite 跑資料庫測試；前端是純 JavaScript 的按鍵導覽 SPA，配合 Cloud Phone 240×320 遠端渲染。Agmarknet 行情從 data.gov.in 每 30 分鐘同步，農業問答在伺服器端呼叫 Gemini 3.5 flash-lite 並限流快取，介面翻譯走 Google Translate；以 systemd 加 nginx 部署，GitHub Actions 跑測試。

**Happy Farm 農產品即時價格** — [zhihao1021/MCH2026-frontend](https://github.com/zhihao1021/MCH2026-frontend)、[MCH2026-backend](https://github.com/zhihao1021/MCH2026-backend)（fork：[frontend](https://github.com/taiwan-hackathon-collection/meichu-2026-cloudmosa--zhihao1021--MCH2026-frontend)、[backend](https://github.com/taiwan-hackathon-collection/meichu-2026-cloudmosa--zhihao1021--MCH2026-backend)）
- 概念：給功能機用的農產品行情服務，同時提供各國官方批發價與小農、盤商自行報價，讓沒有智慧型手機的人也能比價。
- 技術：前端 React 19、TypeScript、Vite 與 SCSS，自寫 useKeypad、useSoftKeys、useListNav 三個 hook 用堆疊管理方向鍵、數字鍵與左右軟鍵。後端 FastAPI 加 SQLAlchemy 2.0 async 與 PostgreSQL，Alembic 管 11 張表，OTP 簡訊登入與 JWT 輪換，APScheduler 依 manifest 排程抓價；官方價格來源做成可插拔 extension，用 pycountry、Babel、phonenumbers 處理多國地區、幣別與電話格式。

**穀價 AgriPrice** — [dw650/2026-MeichuHackathon-CloudMosa](https://github.com/dw650/2026-MeichuHackathon-CloudMosa)（fork：[meichu-2026-cloudmosa--dw650--2026-MeichuHackathon-CloudMosa](https://github.com/taiwan-hackathon-collection/meichu-2026-cloudmosa--dw650--2026-MeichuHackathon-CloudMosa)）
- 概念：CloudMosa 第 3 題「農產品即時價格」。農夫與商販按幾個鍵就看到自己地區當天的價格、30 日走勢、同國各地區比價與 150 公里內最高最低價；缺資料時誠實標示原因。
- 技術：docker compose 四個服務：Caddy 2 反代、FastAPI 後端分三層、APScheduler worker 抓取並正規化資料、PostgreSQL 16。前端 React 加 TanStack Query、zustand 與 i18next，Playwright 與 Vitest 測試；資料來自 data.moa.gov.tw、agmarknet.gov.in、data.gov.my 與世界銀行，GeoIP 判斷使用者國家。

**RailKey** — [j1018y/cloudphone_agent](https://github.com/j1018y/cloudphone_agent)（fork：[meichu-2026-cloudmosa--j1018y--cloudphone_agent](https://github.com/taiwan-hackathon-collection/meichu-2026-cloudmosa--j1018y--cloudphone_agent)；主 repo linskybing/cloudphone 已不公開）
- 概念：在按鍵手機上查印度火車即時動態。按 0 說一句話，就知道最近車站在哪、哪幾班可搭、現在誤點多久；針對月台上不便拿智慧型手機、長途車電量不足、T9 打站名困難的情境。
- 技術：React 加 Vite 的 Cloud Phone widget，用官方 @cloudmosa-inc/cloudphone-types。全部跑在 Cloudflare Workers：Workers AI 做 Whisper 語音辨識與 Qwen3.6-35B-A3B 的 agent 決策，KV 快取上游 RailRadar 查詢，Vectorize 存車站 RAG，cron 每 6 小時預熱種子路線；Playwright 端對端測試，GitHub Actions 自動部署。

**藥丸辨識與用藥紀錄** — [I-Love-Hotpot/meichu-hackathon-2026](https://github.com/I-Love-Hotpot/meichu-hackathon-2026)（fork：[meichu-2026-cloudmosa--I-Love-Hotpot--meichu-hackathon-2026](https://github.com/taiwan-hackathon-collection/meichu-2026-cloudmosa--I-Love-Hotpot--meichu-hackathon-2026)）
- 概念：用功能機拍藥丸就能辨識是什麼藥並記錄用藥，讓長輩或資源有限的使用者不必看懂藥袋。
- 技術：前端 React、Vite 加 i18next，以 nginx 容器提供；後端 Fastify 加 mysql2 連 MariaDB 11，Twilio 發簡訊，Gemini 3.5 flash 生成藥物說明。推論伺服器獨立成 Python 容器：Ultralytics YOLO 偵測並裁切藥丸，MobileNetV3 分類給前三名，PyTorch CPU 版，模型與權重不進後端映像；三份 compose 檔分開開發、正式與推論環境。

### 羅技：MX Creative Console

**Cluck In** — [AppleChen17/Cluck_in](https://github.com/AppleChen17/Cluck_in)（fork：[meichu-2026-logitech--AppleChen17--Cluck_in](https://github.com/taiwan-hackathon-collection/meichu-2026-logitech--AppleChen17--Cluck_in)）
- 概念：住在 MX Creative Console 上的數位雞，替你守住專注時間：偵測你是否分心，用實體按鍵切換閒置、專注與 AI 協助狀態，並代為處理打擾你的訊息。
- 技術：C# 與 .NET 10 monorepo：WPF 桌面程式做專注計時與前景視窗、瀏覽器網址取樣並開 ASP.NET Core HTTP API；Console 插件用 Loupedeck PluginApi 與 SkiaSharp 畫鍵面；外部訊息模組以 Python FastAPI 接 Gmail IMAP 與 Slack Socket Mode，回覆走 SMTP 與 chat.postMessage；AI 引擎以本機 Ollama 跑 Gemma 3，另有 React 網頁面板。

**Moodial V2** — [WongChiChong05/Moodial-V2](https://github.com/WongChiChong05/Moodial-V2)（fork：[meichu-2026-logitech--WongChiChong05--Moodial-V2](https://github.com/taiwan-hackathon-collection/meichu-2026-logitech--WongChiChong05--Moodial-V2)）
- 概念：「描述感覺，轉出結果」。說一句想要的氛圍，AI 找出照片裡該調的物件與控制項，用 Keypad 選物件、Dialpad 轉盤調強度，成品仍是可再編輯的 Photoshop 圖層。
- 技術：Photoshop CEP 面板加 ExtendScript 主機負責建立調整圖層與遮罩；Keypad 與 Dialpad 插件用 C# 的 Logitech Actions SDK；本機 Node 服務以 OpenAI gpt-4.1-mini 解讀編修意圖、onnxruntime-node 做物件分割、sharp 處理影像，三者以有驗證的本機 HTTP 串接，附 PowerShell 建置與測試腳本。

### AMD：Physical AI 與 AI PC

**CAT，Context-Aware boT** — [EthelHsiao/2026-Meichu-Hackthon](https://github.com/EthelHsiao/2026-Meichu-Hackthon)（fork：[meichu-2026-amd--EthelHsiao--2026-Meichu-Hackthon](https://github.com/taiwan-hackathon-collection/meichu-2026-amd--EthelHsiao--2026-Meichu-Hackthon)）
- 概念：會看你工作狀況的實體桌面陪伴貓。你說「作業卡住了」時，它用你剛才做了什麼、卡了多久來回應，而不是泛泛的建議。
- 技術：ESP32 主板用 PlatformIO 與 Arduino 框架，接兩顆 FSR 壓力感測、MPU6050 IMU、1.8 吋 TFT、蜂鳴器與麥克風，另一顆 ESP32-CAM 拍作業；PN54 上的 Python agent 用 mss 截圖、sentence-transformers 加 bge-m3 做記憶 RAG，經 WebSocket 連板子；MI300 伺服器以 ollama/ollama:rocm 容器跑 Qwen 系列模型並用 FastAPI 包 API；語音轉文字為本機 Breeze-ASR-25。

**CSI Collection Lab** — [toshiishere/2026_meichuhackathon](https://github.com/toshiishere/2026_meichuhackathon)（fork：[meichu-2026-amd--toshiishere--2026_meichuhackathon](https://github.com/taiwan-hackathon-collection/meichu-2026-amd--toshiishere--2026_meichuhackathon)）
- 概念：把 WiFi CSI 訊號與攝影機畫面同步採集起來，做成可標註、可訓練、可部署的感測流水線，用無線訊號感知人的動作。
- 技術：docker compose 多服務：React 前端、FastAPI 後端、以 pyserial 收 ESP32 CSI 與 PyAV 收相機的 hardware service、Discord 通知 bot。訓練服務跑 ROCm 10 版 PyTorch 2.13（gfx1152），用 YOLOv8-pose 自動標註影片再微調 CSI 人體活動辨識模型；NPU 服務以 Ryzen AI 1.8 做 XINT8 量化推論，mock 模式無硬體也能跑整套 UI。

**LLM 控制 micro:bit 機器人車** — [buioyc-euuio/2026-meichu-hackathon](https://github.com/buioyc-euuio/2026-meichu-hackathon)（fork：[meichu-2026-amd--buioyc-euuio--2026-meichu-hackathon](https://github.com/taiwan-hackathon-collection/meichu-2026-amd--buioyc-euuio--2026-meichu-hackathon)）
- 概念：打一句「往前走兩秒再右轉」，車子就照做；並讓 LLM 自己把「左轉」校正成剛好 90 度，把校正結果寫成可重用的知識。
- 技術：Python 3.12，bleak 走 BLE 送指令給 micro:bit v2 上 MakeCode 寫的韌體；LLM 用 google-genai 的 Gemini 或本機 Ollama 做 tool calling，另有一版改接 AMD Lemonade Server 的 OpenAI 相容 API；網球追蹤用 YOLO 加傳統 CV 在 GPU 上跑，FastAPI 串流 JSON；語音端有 websockets 加 sounddevice 的 ASR 與 TTS 模組。

**hear tAIgi** — [haleychang0530/2026meichu_hackathon](https://github.com/haleychang0530/2026meichu_hackathon)（fork：[meichu-2026-amd--haleychang0530--2026meichu_hackathon](https://github.com/taiwan-hackathon-collection/meichu-2026-amd--haleychang0530--2026meichu_hackathon)）
- 概念：無障礙優先的台語學習：拍下課本頁面就變成聽與說的練習，學習者、教師與家長各有視角，讓台語多一種被理解的方式。
- 技術：React 加 Vite 前端，FastAPI 核心後端管 SQLite 與課文流程，契約用 JSON Schema 共用。語音閘道以 faster-whisper（CTranslate2）做 ASR、本機 TTS；Local RAG 用確定性 CPU embedding 加來源清單；MI300 上另一個 FastAPI 服務以 vLLM 跑視覺語言模型分析課文影像；雲台版用 Ultralytics 與 pyserial 控制 ESP32，Vitest 與 pytest 測試。

**Harmonix，Live Sound Reference** — [YuTingChen0502/MeiChuHackthon26](https://github.com/YuTingChen0502/MeiChuHackthon26)（fork：[meichu-2026-amd--YuTingChen0502--MeiChuHackthon26](https://github.com/taiwan-hackathon-collection/meichu-2026-amd--YuTingChen0502--MeiChuHackthon26)）
- 概念：給已知歌曲與樂器配置的現場 PA 助手：拿一支房間麥克風和事先上傳的理想參考比對，告訴人哪個聲源偏了；有把握才給數值，永遠不碰混音台。
- 技術：Python 音訊管線：sounddevice 取麥克風、共用 PCM 分窗與品質檢查，InstrumentAnalyzer 用 PyTorch 加 Demucs 分離聲源產生 AnalyzerEvidence，核心層算偏差、校準信心與棄權；Starlette 加 websockets 提供本機 HTTP 與 WebSocket 給操作者主控台，契約以 JSON Schema 驗證，模型 bundle 有版本與驗收紀錄，目標硬體 MI300 與 PN54。

**Fridge Guardian** — [yunhung0806/2026_meichu_hackathon](https://github.com/yunhung0806/2026_meichu_hackathon)（fork：[meichu-2026-amd--yunhung0806--2026_meichu_hackathon](https://github.com/taiwan-hackathon-collection/meichu-2026-amd--yunhung0806--2026_meichu_hackathon)）
- 概念：隱私優先的共享冰箱守衛：拍到人和手上的東西，選放入或取出，就知道這件是誰的，非擁有者取用時警示。
- 技術：Python 套件加 FastAPI station API，OpenCV 取像；身分用 YuNet 偵測加 SFace 比對，物品由 loopback 的 item-vision sidecar 以 Grounding DINO 框選、CLIP 出候選、DINOv2 排序，ONNX 在 PN54 上跑；所有權策略與紀錄存 SQLite。可選後端接 Lemonade 提供的 Gemma 3 做本機 RAG；前端 React 加 Drizzle，用 Cloudflare vite plugin 部署。

### 聚陽實業：一句話讀懂消費者

**潮會搭** — [shangjung1012/matching-outfit](https://github.com/shangjung1012/matching-outfit)（fork：[meichu-2026-makalot--shangjung1012--matching-outfit](https://github.com/taiwan-hackathon-collection/meichu-2026-makalot--shangjung1012--matching-outfit)；副本 sjtseng0924/matching-outfit）
- 概念：把場合、預算、天氣、偏好和已有衣物一次講清楚，就拿到成套且可解釋的穿搭，還能虛擬試穿。
- 技術：Vue 3 加 TypeScript 前端，FastAPI 後端，PostgreSQL 加 pgvector 存向量。檢索用 FashionCLIP 做圖文 embedding，查詢規劃與美感審查呼叫 OpenAI（gpt-5.6-terra、gpt-4.1-mini）。GPU 端另一組 compose：虛擬試穿服務加 LHM++ 人體 3D 重建（CUDA 12.8、PyTorch3D、Gaussian Splats），MinIO 存檔，經 Cloudflare Tunnel 對外，前端以 gaussian-splats-3d 顯示。

**一句穿搭 v2** — [petercechung/outfit-agent](https://github.com/petercechung/outfit-agent)（fork：[meichu-2026-makalot--petercechung--outfit-agent](https://github.com/taiwan-hackathon-collection/meichu-2026-makalot--petercechung--outfit-agent)）
- 概念：說一句「下週一面試，想要簡約但不要太死板」，就從 11,636 件 H&M 真實商品組出三套可購買的穿搭，每件有理由，再說一句就能換。
- 技術：TypeScript 寫的 Cloudflare Worker，靜態前端由 Assets 提供；商品、向量與縮圖放 R2，請求歷史與 v1 的需求訊號各存一個 D1。造型師 agent 與視覺評審用 OpenAI gpt-5.4-mini，embedding 用 text-embedding-3-small；FashionCLIP 編碼器以 open_clip 包成 Cloudflare Container 內的 Python 服務；Biome 檢查、Vitest 測試。

**LookLine** — [JacobLinCool/lookline](https://github.com/JacobLinCool/lookline)（fork：[meichu-2026-makalot--JacobLinCool--lookline](https://github.com/taiwan-hackathon-collection/meichu-2026-makalot--JacobLinCool--lookline)）
- 概念：「推薦你買什麼，讓你穿得出來」。點、線、面：對話幫你買到對的單品，衣櫃變成持續創作造型的遊戲，再讓大家一起創作把趨勢擴散出去。
- 技術：TypeScript monorepo：React 加 vinext 的 App Router 跑在 Cloudflare Workers，Drizzle 定義 schema、D1 存資料、R2 存生成圖，每日 cron 產清單。engine 套件做意圖解析、排序、回饋與創作，文字用 Gemini 3.5 flash-lite 或 gpt-5.6-luna 並設逾時降級，生圖用 gemini-3.1-flash-image，判別式問題交給 TypeSafe Jev；另有 H&M 資料匯入與 1,200 名模擬使用者的評估套件。

**Consumer Intent Agent** — [chrislaiisme/mchackathon2026](https://github.com/chrislaiisme/mchackathon2026)（fork：[meichu-2026-makalot--chrislaiisme--mchackathon2026](https://github.com/taiwan-hackathon-collection/meichu-2026-makalot--chrislaiisme--mchackathon2026)）
- 概念：隊名「勢在必得」。一句話變成結構化、可解釋的購衣意圖，找出商品並畫出原創概念圖，逐輪依回饋改進，改進幅度用可驗證的分數呈現。
- 技術：FastAPI 後端加 Next.js 與 shadcn 前端。ENGINE 01 用 gpt-4o-mini 結構化輸出產生意圖 JSON；ENGINE 02 在 KAGL 服飾目錄上做 FashionCLIP embedding 加自寫 BM25 的混合檢索，sentence-transformers 交叉編碼器與 Qwen3-VL-8B reranker 重排，每項分數可拆解；語音輸入用 faster-whisper，去背用 rembg 與 BiRefNet，另整合 MCP servers。

### NXP：FRDM-i.MX93 邊緣 AI

**edge-gesture-control** — [yanhongioi/edge-gesture-control](https://github.com/yanhongioi/edge-gesture-control)（fork：[meichu-2026-nxp--yanhongioi--edge-gesture-control](https://github.com/taiwan-hackathon-collection/meichu-2026-nxp--yanhongioi--edge-gesture-control)）
- 概念：用 FRDM-i.MX93 不碰電腦就控制電腦：手勢在板上毫秒級辨識，語音指令由 PC 上的本地 LLM 理解。
- 技術：板端 Python 用 tflite_runtime 加 Ethos-U delegate，MobileNet SSD 手部與人物偵測、21 點骨架與 MobileNetV3 量化模型都經 Vela 編譯到 NPU，OpenCV 抓 C270 影像，結果經 paho-mqtt 發布並可 HTTP 串流或 HDMI 顯示；語音喚醒用 NXP AFE 與 VIT，MG996R 伺服雲台走硬體 PWM。PC 端用 faster-whisper 加 silero-vad 做語音，Ollama 本地 LLM 解析指令再操作游標與視窗。

**SmartDrawer** — [Apollo58168/2026_Hackathon_NXP](https://github.com/Apollo58168/2026_Hackathon_NXP)（fork：[meichu-2026-nxp--Apollo58168--2026_Hackathon_NXP](https://github.com/taiwan-hackathon-collection/meichu-2026-nxp--Apollo58168--2026_Hackathon_NXP)）
- 概念：會自己記帳的抽屜：開關抽屜時看出哪個位置的東西變了，只辨識那一塊並更新庫存，還能用語音問抽屜。
- 技術：純 Python 跑在 FRDM-i.MX93：MiDaS v2.1 Small 深度模型與 GoPoint SSDLite、YOLOv8 int8 的 TFLite 模型皆經 Vela 編譯在 Ethos-U 上驗證，OpenCV 取 C270 影像做 A/B 深度差找變更區域再裁切辨識；C270 麥克風做喚醒詞與英文 ASR，語意對應到品項，SQLite 存庫存，HDMI 介面顯示；附 PC 端確定性模擬與 pytest 測試。

**Fieldbound** — [milktea7654/2026-meichu](https://github.com/milktea7654/2026-meichu)（原 repo 已轉私有或刪除，未能 fork）
- 概念：在 FRDM-i.MX93 上跑的離線戶外 RPG：真實地圖切成每格 2,500 平方公尺，走到就永久點亮，每六個新格觸發劇情事件。
- 技術：Python 3.11 套件 edge_rpg，板端 UI 用 pygame-ce 加 SDL2，世界狀態與方格存 SQLite，離線地圖用 MBTiles；瀏覽器模擬器提供 OpenStreetMap 底圖、瀏覽器定位與 Android GPS Bridge，模擬與真實定位分開資料庫；相機、麥克風與 NPU 場景模型列在驗收追蹤中尚未真機驗收。

**Ward Monitor** — [kiki0518/ward-monitor](https://github.com/kiki0518/ward-monitor)（fork：[meichu-2026-nxp--kiki0518--ward-monitor](https://github.com/taiwan-hackathon-collection/meichu-2026-nxp--kiki0518--ward-monitor)）
- 概念：病房監測：開發板相機即時看床位、姿勢推論偵測異常，並把生理數據自動整理成交班紀錄。
- 技術：開發板端 Python 直接轉送相機 MJPEG，並用 MoveNet 做姿勢推論；FastAPI 後端以 websockets 接收與分發影像、提供床位與模擬生理數據的 REST 與 WebSocket、paho-mqtt 收訊、fpdf2 出 PDF，AI 交班紀錄呼叫 TAIDE 模型；前端 React、Vite、Tailwind 與 Recharts 畫圖。

### 愛德萬測試：ACS RTDI 即時測試資料

**Advantest AI Monitor Plugin** — [mchien728/Hackathon-Advantest-grp1](https://github.com/mchien728/Hackathon-Advantest-grp1)（fork：[meichu-2026-advantest--mchien728--Hackathon-Advantest-grp1](https://github.com/taiwan-hackathon-collection/meichu-2026-advantest--mchien728--Hackathon-Advantest-grp1)）
- 概念：測試機台的即時監控插件：發現異常的晶圓測試模式、預測感測器結果、視覺化並主動寄警示。
- 技術：三層部署在 te-cloud 沙盒：SmarTest 8 的 Java 測試程式跑在 HC 虛擬機，Edge 端以官方 oneAPI Python 3.10 容器接收 ACS 事件並用 scikit-learn 與 Ridge 模型偵測異常、預測感測值，前端 Flask 儀表板透過 SSH 隧道取資料、以 OpenRouter 呼叫模型產生說明、resend 寄 Gmail 警示；含訓練腳本與資料集。

**ACS RTDI 全端系統** — [wendy912512/advantest-hackathon-fullstack](https://github.com/wendy912512/advantest-hackathon-fullstack)（fork：[meichu-2026-advantest--wendy912512--advantest-hackathon-fullstack](https://github.com/taiwan-hackathon-collection/meichu-2026-advantest--wendy912512--advantest-hackathon-fullstack)）
- 概念：把 SmarTest 的即時測試資料變成看得懂的網頁：異常監控、趨勢、晶圓分布圖與溫度預測，附名詞對照讓外行也能讀。
- 技術：後端 FastAPI 接 OneAPI 即時事件回呼，資料組裝後以 WebSocket 串流，異常偵測與溫度預測用 LightGBM 與 scikit-learn，訓練過程在 Jupyter notebook；前端 Next.js 加 shadcn、Tailwind 與 Recharts 畫晶圓圖與趨勢，axios 取資料；可匯入官方 RawResult CSV 離線重播。

**溫度預測（場景二）** — [LiLOUIS0803/advantest_mchack2026](https://github.com/LiLOUIS0803/advantest_mchack2026)（fork：[meichu-2026-advantest--LiLOUIS0803--advantest_mchack2026](https://github.com/taiwan-hackathon-collection/meichu-2026-advantest--LiLOUIS0803--advantest_mchack2026)）
- 概念：RTDI 題目「場景二：溫度預測」：機台在測試流程六個時間點問「sensor k 等一下幾度」，用前面測完的測項預測出來。
- 技術：推論核心只依賴 numpy，六個模型權重以 pickle 存放，用 pandas 與 scikit-learn 在 25 片晶圓 CSV 上訓練並做 leave-wafer-out 評估；scene2_hook 黏到官方 oneAPI sample 的 Python 3.10 容器，另有 CSV 串流回放與假 NexusData 事件解析測試、SmarTest 8.7 Java 測試專案與 Flask 網頁儀表板。沒有 README。

**即時異常偵測儀表板** — [Ken0626/mchackathon-advant-lab](https://github.com/Ken0626/mchackathon-advant-lab)（fork：[meichu-2026-advantest--Ken0626--mchackathon-advant-lab](https://github.com/taiwan-hackathon-collection/meichu-2026-advantest--Ken0626--mchackathon-advant-lab)）
- 概念：即時異常偵測儀表板：邊測邊看良率、site 之間是否不平衡，出事時給出動作建議，並預測溫度。
- 技術：Python 3 接官方 libACSAction 與 liboneAPI 共享庫收 RTDI 事件，window_features 算滑動視窗特徵，scikit-learn Isolation Forest 與基準模型判異常、另訓練溫度預測器並存成 pickle；simulate_stream 每 0.3 秒改寫 dashboard_status.json，靜態 HTML 儀表板只讀這個檔案，前後端完全解耦，附 Dockerfile。沒有 README。

### Google：Gemini AI Agent

**急救副駕 First Aid Copilot** — [matthiola0/mchackathon](https://github.com/matthiola0/mchackathon)（fork：[meichu-2026-google--matthiola0--mchackathon](https://github.com/taiwan-hackathon-collection/meichu-2026-google--matthiola0--mchackathon)；副本 Shih-Hsuan/first_aid_copilot、EricHuang0302/mchackathon）
- 概念：「派遣員指揮，Agent 輔助」：緊急事件通報時 Agent 幫忙整理現場資訊、協調附近 AED、交接給救護單位，讓人專心指揮。
- 技術：Agent 服務用 Flask 加 flask-sock、gunicorn 與 PostgreSQL 16，以 Google ADK 與 google-genai 呼叫 Gemini：語音轉錄用 gemini-3.5-transcribe-live，文字用 gemini-3.8-flash；急救規則以 YAML 存放並經 JSON Schema 驗證。前端 React、Vite、MUI 與 react-google-maps 顯示地圖與 QR code，docker compose 一鍵啟動。

**NCKU Smart Commute 成大智慧通勤** — [JKaiWang/2026MC_Hackathon_PharLawEngineer](https://github.com/JKaiWang/2026MC_Hackathon_PharLawEngineer)（fork：[meichu-2026-google--JKaiWang--2026MC_Hackathon_PharLawEngineer](https://github.com/taiwan-hackathon-collection/meichu-2026-google--JKaiWang--2026MC_Hackathon_PharLawEngineer)；副本 KimmyTsai、Bigpig8787）
- 概念：成大校園通勤 Agent：問「4264 教室在哪」就查到大樓樓層、剩餘車位、YouBike、路況與下一堂課，還能拍門牌確認位置。
- 技術：Python 3.13 加 google-adk 2.9，模型 gemini-3-flash-preview，可切換 Ollama 的 gemma3:4b 本機模型與 Vertex AI；工具層用 requests 與 aiohttp 打成大 GIS、校園停車、YouBike、TDX 路況與中央氣象署 API，PROVIDER_MODE 可切 fixture 離線模式；ntfy 推播提醒，adk web 除錯介面，410 項 pytest 不需網路，附 Dockerfile。

**信用卡回饋推薦** — [gainsborouo/meichu-hackathon-2026](https://github.com/gainsborouo/meichu-hackathon-2026)（fork：[meichu-2026-google--gainsborouo--meichu-hackathon-2026](https://github.com/taiwan-hackathon-collection/meichu-2026-google--gainsborouo--meichu-hackathon-2026)）
- 概念：告訴你這筆消費該刷哪張卡：匯入十張台灣信用卡的回饋規則與消費紀錄，登入後加入持有的卡就有推薦。
- 技術：後端 Python 3.13、FastAPI 加 SQLAlchemy async 與 PostgreSQL，Alembic 遷移，推薦 agent 用 google-adk 2.9 加 skills 目錄，模型為 Gemini 3.7 flash，透過自架的 OpenAI 相容 LLM gateway（copilot-api 容器）呼叫，ddgs 查網頁；前端 Vue 3 加 Pinia、vue-i18n 與 Tailwind，Firebase 與 Google 登入，另有 WXT 打包的瀏覽器擴充功能，Caddy 提供靜態檔。組別依技術推斷為 Google。

**長輩陪伴對話** — [ponponnnnnn/2026MCH](https://github.com/ponponnnnnn/2026MCH)（fork：[meichu-2026-google--ponponnnnnn--2026MCH](https://github.com/taiwan-hackathon-collection/meichu-2026-google--ponponnnnnn--2026MCH)）
- 概念：陪獨居長輩聊天的 App：依健檢清單與話題規則主動開場、轉換話題、記住長輩的狀況，讓對話有溫度也有依據。
- 技術：Flutter App 用 record 錄音、flutter_pcm_sound 播放，經 WebSocket 把 PCM 音訊串到後端；Node 22 加 TypeScript 的 Express 後端以 @google/genai 接 Gemini Live（gemini-3.8-live）做即時語音對話，gemini-flash 產生報告，Firestore 存長輩檔案，pdfkit 出 PDF、nodemailer 寄給家屬；家屬儀表板為 React 加 Recharts。沒有頂層 README，組別依技術推斷為 Google。

### 創客交流組：新竹市 AI 領航青年數位工具補助與資安

**梅竹通** — [zhuang768/Leo-zhuang-](https://github.com/zhuang768/Leo-zhuang-)（fork：[meichu-2026-hsinchu-maker--zhuang768--Leo-zhuang-](https://github.com/taiwan-hackathon-collection/meichu-2026-hsinchu-maker--zhuang768--Leo-zhuang-)；後端 zhuang768/meizhutong-sheets）
- 概念：青年端 iOS App：把「新竹市 AI 領航青年數位工具補助」的申請資料與文件一次備齊，並查案件狀態與補件提示；明確聲明不是市府正式入口。
- 技術：Swift 原生 iOS App，XcodeGen 產生專案，Apple Vision 框架在裝置端辨識身分證與帳單，含單元與 UI 測試；後端 meizhutong 原型是 TypeScript 的 Cloudflare Worker，D1 存案件、KV 存檔案、Assets 提供承辦人主控台；姊妹 repo meizhutong-sheets 加上試算表匯出與以 OpenAI gpt-4o 做 AI 稽核的 Node 測試腳本。

**竹青安心GO** — [zhuang768/auxin-](https://github.com/zhuang768/auxin-)（fork：[meichu-2026-hsinchu-maker--zhuang768--auxin-](https://github.com/taiwan-hackathon-collection/meichu-2026-hsinchu-maker--zhuang768--auxin-)）
- 概念：青年把內容送進 ChatGPT、Claude、Gemini 前，先在自己裝置上抓出個資、解釋風險並給安全改寫；市府只看到匿名彙總。
- 技術：Chrome Manifest V3 擴充功能，純 JavaScript 分 adapter、detector、masker 與風險抽屜四層，個資偵測全在本機；後端 FastAPI 加 Jinja2 樣板與 SQLite，itsdangerous 管 session，案件狀態機、市府工作台與站內通知，LINE Messaging API 以 dry-run 模式串接，憑證用 HMAC 簽章加 nonce，附 reset 與 readiness 檢查腳本。

**資安無慮** — [Lee-Yi-Syuan/Hackthon](https://github.com/Lee-Yi-Syuan/Hackthon)（fork：[meichu-2026-hsinchu-maker--Lee-Yi-Syuan--Hackthon](https://github.com/taiwan-hackathon-collection/meichu-2026-hsinchu-maker--Lee-Yi-Syuan--Hackthon)）
- 概念：不另開宣導頁，把資安教育拆進補助流程的申請、綁定、審核、核銷、撥款五關，在使用者真的會遇到風險的那一刻讓他經歷一次。
- 技術：單一 HTML 檔，無建置流程與相依套件，hash 路由讓瀏覽器上一頁可用，狀態存 localStorage 並在失敗時降級為記憶體；全站 CSS 權杖支援深色模式，手機優先，懶人包與檢核聲明書有 A4 列印樣式；匯率介接有內建備援值；以 Cloudflare Workers 靜態資產部署，GitHub Actions 推 main 自動更新。

**松客黑竹梅：AI 補助申請小幫手與智慧審核後台** — [ExpertsHan/mchackathon2026](https://github.com/ExpertsHan/mchackathon2026)（fork：[meichu-2026-hsinchu-maker--ExpertsHan--mchackathon2026](https://github.com/taiwan-hackathon-collection/meichu-2026-hsinchu-maker--ExpertsHan--mchackathon2026)）
- 概念：把補助申請走成一條線：擴充功能先擋資安風險，AI 小幫手陪民眾申請，智慧審核後台幫承辦人比對並提建議，但核定一律由人決定。
- 技術：申請小幫手：Next.js 加 Radix UI 前端，FastAPI 後端加 SQLAlchemy 與 pgvector 存知識向量，pypdf 讀文件，模型可切 Gemini 3.7 flash 或 gpt-5.6-luna。審核後台：Express 加 better-sqlite3，multer 收檔，Gemini 2.5 flash 做 OCR，規則引擎 RULE-001 到 020，@line/bot-sdk 主動通知；另有 Chrome 擴充功能與 docker compose 一鍵啟動腳本。

**竹青 AI 安心辦** — [ShaoChiLin/hc-ai-pass-websites](https://github.com/ShaoChiLin/hc-ai-pass-websites)（fork：[meichu-2026-hsinchu-maker--ShaoChiLin--hc-ai-pass-websites](https://github.com/taiwan-hackathon-collection/meichu-2026-hsinchu-maker--ShaoChiLin--hc-ai-pass-websites)）
- 概念：黑客松展示用的靜態網站集合：漫畫式吉祥物房間當入口，點亮電腦就進入服務選單，子站示範補助申請流程。
- 技術：原生 HTML、CSS、JavaScript，無套件無建置，GitHub Pages 發布；home.js 處理螢幕四角投影、放大返回與焦點管理，particles.js 畫游標粒子與電路折線並在閒置時停止，支援 Escape、瀏覽器上一頁與減少動態效果設定；吉祥物圖以生成工具製作並用 CSS 交替播放，附測試目錄。

**Ctrl & Create** — [redfish-27182/hackson-Ctrl-Create](https://github.com/redfish-27182/hackson-Ctrl-Create)（fork：[meichu-2026-hsinchu-maker--redfish-27182--hackson-Ctrl-Create](https://github.com/taiwan-hackathon-collection/meichu-2026-hsinchu-maker--redfish-27182--hackson-Ctrl-Create)）
- 概念：新竹市補助申請與資安教育網站：申請頁加 AI 聊天，並用一段附手機模擬器的互動遊戲教申請人辨識風險。
- 技術：前端 React 加 Vite、Tailwind、react-router、swiper 輪播與 driver.js 導覽，遊戲有手機模擬器與像素打字機元件；後端 Flask 加 flask-cors 與 SQLite，Gemini 讀取收據與回答聊天，subsidy_checker 用規則判補助資格，並以 LINE Bot SDK v3 接 webhook；README 只有團隊守則，9 月 2 日建立。

### 組別不明

（確定為本屆作品但看不出組別的 repo 已依技術推斷歸入上方各組；仍無法判斷的列在下方「很可能或存疑」。）


## 很可能或存疑，未 fork

- [handsonli2468/mc_hackathon_2026](https://github.com/handsonli2468/mc_hackathon_2026)（AMD，很可能）：機器人任務規劃、行為樹與 VLM 視覺辨識系統；[Latuuuuu/Hackathon-vision-server-vlm](https://github.com/Latuuuuu/Hackathon-vision-server-vlm) 是跑在 AMD GPU 上的視覺 VLM server，疑為同隊。
- [dhggdhfnjd/mc_v2](https://github.com/dhggdhfnjd/mc_v2)（CloudMosa，很可能）：Mizani，給肯亞與烏干達邊境小農的 Cloud Phone 農價議價助手；同作者另有 mizani、guardian-rogue。
- [vitoface/cloudphone-2025meichuhackathon-demo-main](https://github.com/vitoface/cloudphone-2025meichuhackathon-demo-main)（CloudMosa，很可能）：由官方 demo 複製，三人於 9 月 17 至 20 日開發，未寫明題目。
- [Aquatictw/Hackathon_YJSNPI](https://github.com/Aquatictw/Hackathon_YJSNPI)（愛德萬，很可能）：grp6 RTDI test assistant，含預測、偵測與後端分工文件。
- [ChengEnYu0428/PawPal_Local_Assist](https://github.com/ChengEnYu0428/PawPal_Local_Assist)（組別不明，很可能）：以 Ollama 與 Gemma 在本機看螢幕的桌面陪伴助理，README 提到梅竹簡報；同作者另有 livekit-unity-hackathon。
- [BumbleBee-100/Cloud-Mini](https://github.com/BumbleBee-100/Cloud-Mini)、DHur（CloudMosa，存疑）：Cloud Phone 瀏覽器 widget，但於截止後建立且未提活動。
- [CasperHsu/vision-parking](https://github.com/CasperHsu/vision-parking)（創客組，存疑）：新竹市停車場即時空位查詢，未提活動。
- [ZiyanGZiyaNG/meichu-doc](https://github.com/ZiyanGZiyaNG/meichu-doc)、[Chen-Yu-Chang/Hackathon_Karmate](https://github.com/Chen-Yu-Chang/Hackathon_Karmate)（存疑）：前者只有一個空 commit，後者 9 月 12 日建立且未提活動。

## 資料來源與方法

候選來自 GitHub 的關鍵字、README 與 code search、贊助商範例 repo 的 fork、GH Archive 的比賽期間事件，以及 5.6 萬名 profile 在台灣的帳號在 9 月建立的 repo；共對兩萬多個 repo 抓 metadata、四千篇 README 評分，人工複核約一百個並以 REST API 取得 commit 時間線。完整流程、腳本與判定表見 [scanner](https://github.com/taiwan-hackathon-collection/scanner) 的 `references/`。
