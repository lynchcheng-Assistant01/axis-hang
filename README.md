# AXIS Gallery — Hanging Planner 布展規劃

互動式布展規劃單頁網站。點平面圖的牆（或文字）→ 捲到對應立面 → 輸入畫作「高 × 寬 × 數量」→ 自動均分上牆、可拖曳微調 → 輸出印有 AXIS GALLERY 的 PDF（統計頁 + 各牆放樣座標）。**該 PDF 可拖回網頁繼續編輯**（狀態 JSON 內嵌於 PDF 附件 + Subject 雙備援），另有 JSON 匯出/匯入保險。

## 幾何（來自 260713 CAD 圖）

- 牆長（cm）：A=330 · B=425 · C=430 · D=400 · E=270 · F=320 · G=500；Column 1–6 每面寬 60（四根柱的六個預掛面）
- 立面（全面共用）：總高 323；0–22 Air Vent 帶；22–256 可掛區（高 234）；256–323 頂帶
- 尺寸輸入慣例：**高 × 寬**
- 垂直規則：展示區垂直置中（中心 139）/ 齊頂線（可設高度）；拖曳後自由，snap 0.5cm

## 本機預覽

```bash
cd ~/LynchAssistant/studiox4-web/axis-gallery-planner
python3 -m http.server 8788 --bind 127.0.0.1
# → http://127.0.0.1:8788/
```

## 檔案

- `index.html` — 全部邏輯（無 build step；分節 CONFIG / STATE / LAYOUT / DRAG / PDF-EXPORT / IMPORT）
- `assets/plan.png` — 平面圖底圖（源：Downloads/260713_布展畫作平面-設計平面圖 (2).pdf，qlmanage 3000px 轉檔+裁邊）
- `vendor/pdf-lib.min.js` — pdf-lib 1.17.1 UMD（vendored，可離線）
- `_dev/` — 開發用 spike（不部署）

## Hotspot 校正

網址加 `?calibrate=1` → 點平面圖會在 console 印出原圖像素座標，對照 `HOTSPOTS` 常數修改。

## 部署（GitHub Pages）

```bash
gh repo create axis-hang --public --source . --push
gh api repos/{owner}/axis-hang/pages -X POST -f 'source[branch]=main' -f 'source[path]=/'
```
