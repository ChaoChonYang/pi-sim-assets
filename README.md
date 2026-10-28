# pi-sim-assets

樹莓派模擬器（pi-sim.html）上課用的素材鏡像。模擬器會先從這裡下載，失敗才改用公開 CDN。

| 檔案 | 用途 | 大小 |
|---|---|---|
| skulpt/skulpt.min.js、skulpt-stdlib.js | 瀏覽器裡執行 Python（Skulpt 1.2.0） | 約 1 MB |
| three/three.min.js | 3D 場景（three.js r128） | 0.6 MB |
| ort/ort.wasm.min.js、ort-wasm-simd.wasm、ort-wasm.wasm | ONNX Runtime Web 1.17.3（YOLO 推論） | 約 20 MB |
| models/yolov8n.onnx | YOLOv8n 物件偵測模型（COCO 80 類，640×640） | 12.8 MB |

## 設定步驟

1. 在 GitHub 建立**公開**的 repository，名稱建議用 `pi-sim-assets`。
2. 把這個資料夾裡的所有檔案（含 `.nojekyll`）照原本的資料夾結構上傳到 `main` 分支。
   網頁上傳一次最多 100 個檔案、單檔 25 MB，這些檔案都在範圍內。
3. 到 Settings → Pages，Source 選「Deploy from a branch」，Branch 選 `main`、資料夾選 `/ (root)`，按 Save。
4. 等一兩分鐘，用瀏覽器開這個網址確認能下載：
   `https://你的帳號.github.io/pi-sim-assets/models/yolov8n.onnx`
5. 讓模擬器使用這個網址，任選一種：
   - 編輯 pi-sim.html，搜尋 `ASSET_BASE_DEFAULT`，填入 `"https://你的帳號.github.io/pi-sim-assets/"`（全班都適用，建議）。
   - 或在模擬器終端機輸入 `assets set https://你的帳號.github.io/pi-sim-assets/`（只對這台電腦有效）。
   - 或用網址參數開啟：`pi-sim.html?assets=https://你的帳號.github.io/pi-sim-assets/`

## 上課前檢查

在模擬器終端機輸入：

- `assets test`：逐一檢查每個檔案是否下載得到。
- `assets`：顯示目前每個元件是從「你的 GitHub」還是「公開 CDN」載入。

模擬器下載順序：你的 GitHub Pages → 同一個 repo 的 jsDelivr 鏡像（cdn.jsdelivr.net/gh/帳號/pi-sim-assets@main/）→ 公開 CDN。
YOLO 模型都下載不到時，可以在攝影鏡頭卡片按「選本機模型檔」，直接選 `models/yolov8n.onnx`。

## 授權

- Skulpt：MIT（licenses/skulpt-LICENSE.txt）
- three.js：MIT（licenses/three-LICENSE.txt）
- ONNX Runtime Web：MIT，© Microsoft Corporation（https://github.com/microsoft/onnxruntime）
- YOLOv8n 模型權重：Ultralytics，AGPL-3.0（licenses/yolov8n-AGPL-3.0.txt）。
  ONNX 檔取自 https://github.com/Hyuto/yolov8-onnxruntime-web 。教學使用沒有問題；
  若要把模型放進商業或不公開原始碼的產品，需要另外取得 Ultralytics 的商業授權。
