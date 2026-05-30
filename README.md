# 🎸 和弦疾行者 — Chord Runner

一款以和弦辨識為核心的跑酷節奏遊戲。障礙物從右側滑來，在判定時機按下正確的和弦按鈕讓角色跳過！

![Game Preview](https://img.shields.io/badge/Platform-Browser-00f5ff?style=flat-square) ![License](https://img.shields.io/badge/License-MIT-ff006e?style=flat-square)

---

## 🚀 快速部署到 GitHub Pages

### 步驟 1：建立 Repository

```bash
# 在 GitHub 建立一個新的 repo，例如：chord-runner
# 然後 clone 到本地
git clone https://github.com/你的帳號/chord-runner.git
cd chord-runner
```

### 步驟 2：放入檔案

把以下結構放入 repo：

```
chord-runner/
├── index.html          ← 主遊戲檔案（本檔）
├── README.md           ← 說明文件
└── audio/              ← 音樂資料夾（可選）
    ├── neon_highway.mp3
    └── 你的歌曲.mp3
```

> **注意**：`audio/` 資料夾是選填的。沒有 MP3 的話，遊戲會自動切換到內建的合成音效。

### 步驟 3：啟用 GitHub Pages

1. 在 GitHub repo 頁面，點選上方的 **Settings**
2. 左側選單找到 **Pages**
3. Source 選擇 **Deploy from a branch**
4. Branch 選 `main`，資料夾選 `/ (root)`
5. 點 **Save**

約 1-2 分鐘後，網站會發布到：
```
https://你的帳號.github.io/chord-runner/
```

### 步驟 4：上傳並推送

```bash
# 把所有檔案加入 git
git add .
git commit -m "🎵 初始部署：和弦疾行者"
git push origin main
```

---

## 🎮 遊戲操作

| 操作 | 說明 |
|------|------|
| 點擊和弦按鈕 | 觸控或滑鼠點擊 |
| 鍵盤快捷鍵 | 按鈕上方標示的按鍵（1-7, Q-U, A-H, Z-V 等）|
| ESC | 暫停 / 繼續 |
| 橫向模式 | 手機請旋轉為橫向，效果最佳 |

### 判定規則

- **PERFECT** ✅：在障礙物到達判定線時（黃色光柱閃爍），按下**正確**的和弦
- **MISS** ❌：障礙物到達判定線，但按了**錯誤**和弦，或完全沒有按
- **自由試音** 🎵：沒有障礙物時按任何按鈕都會發出聲音，**不扣分**

---

## ⚙️ 後台管理

在選歌畫面點擊右上角 **⚙ 後台管理**，預設密碼：`admin`

### 新增歌曲流程

1. 填寫歌曲資訊（名稱、演出者、BPM、時長）
2. 設定音頻路徑（例如：`audio/mysong.mp3`）
3. 選擇難度（1-5 顆星）
4. 勾選要啟用的和弦
5. 設定**按鈕顯示模式**：
   - 🎯 只顯示本曲和弦（適合教學用，畫面簡潔）
   - 🎹 顯示全部 30 個（適合進階玩家，本曲無關的和弦會半透明）
6. 上傳 MP3 自動分析（或手動編輯 Beatmap）
7. 儲存後點 **📤 匯出 JSON**，複製設定

### MP3 自動分析說明

- 使用瀏覽器內建 Web Audio API 進行 **FFT 頻譜分析 + 色度圖（Chromagram）比對**
- 每 1.5 秒分析一次，自動產生和弦時間點草稿
- **準確度為中等**，建議分析後手動調整 Beatmap
- 分析完全在瀏覽器本地進行，不上傳任何資料

### 將歌曲設定永久保存

後台資料暫存在瀏覽器 `localStorage`。若要讓設定跟著 GitHub 專案走：

1. 後台點 **📤 匯出 JSON**
2. 複製 JSON 內容
3. 在 `index.html` 找到以下程式碼：

```javascript
const DEFAULT_SONGS = [
  // ... 預設歌曲
];
```

4. 把複製的 JSON 陣列內容貼進去取代
5. 重新 `git push` 即可永久保存

---

## 🎵 30 個支援和弦

| 類型 | 和弦 |
|------|------|
| 大調 | C, D, E, F, G, A, B |
| 小調 | Cm, Dm, Em, Fm, Gm, Am, Bm |
| 屬七 | C7, D7, E7, G7, A7, B7 |
| 大七 | Cmaj7, Fmaj7, Gmaj7, Amaj7 |
| 小七 | Am7, Dm7, Em7, Bm7 |
| 掛留四 | Gsus4, Asus4 |

---

## 📁 專案結構

```
chord-runner/
├── index.html     # 單一檔案包含遊戲、後台、所有樣式與邏輯
├── README.md      # 本說明文件
└── audio/         # 放置 MP3 音樂檔（路徑需與後台設定一致）
```

---

## 🛠️ 技術細節

- **純前端**：零後端、零框架、零 npm，單一 HTML 檔案
- **音效**：有 MP3 時播放 MP3；無 MP3 時使用 Web Audio API 合成音
- **儲存**：歌曲設定存於 `localStorage`，可匯出 JSON 版控
- **和弦發音**：三角波分解和弦琶音（triangle wave arpeggio）
- **手機支援**：偵測直向時顯示旋轉提示，所有按鈕觸控目標 ≥ 48px

---

## 🔧 常見問題

**Q：音樂播放不出來？**
A：確認 MP3 路徑正確，且檔案已上傳到 `audio/` 資料夾。GitHub Pages 區分大小寫。

**Q：手機上按鈕太小？**
A：請使用橫向模式，並確保瀏覽器沒有縮放。

**Q：MP3 分析結果不準確？**
A：Web Audio API 的和弦辨識受錄音品質、編曲複雜度影響。建議分析後手動調整時間點和和弦名稱。

**Q：後台密碼忘記了？**
A：預設密碼是 `admin`，可在 `index.html` 搜尋 `ADMIN_PASS` 修改。

---

Made with 🎵 and ☕ — [Chord Runner](https://github.com/你的帳號/chord-runner)
