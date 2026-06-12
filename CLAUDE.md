# CLAUDE.md — R-Wei Studio 作品集 / 接案站 交接書

> 全隊共用的進場背景文件。任何人(或 AI)進到 `portfolio-site/` 先讀這份，再動手。
> 最後更新：2026-06-12（大改版 v2 完成）。
>
> 📌 **維護規則**：有大改動（新增頁面、改部署/網域、改報價方案、大幅改版）完工後同步更新本檔與「最後更新」日期。

---

## 1. 這是什麼

張育瑋（R-Wei Studio）的**個人作品集 + 接案行銷網站**，正式網域 **https://rwei-studio.com**。
純靜態網站，無框架、無建置步驟、無後端 —— 就是幾支手寫 HTML（CSS 全部 inline 在 `<style>` 內）。

三個對外身分要分清楚：
| 名稱 | 用途 |
| --- | --- |
| **R-Wei Studio** | 對外接案品牌（`freelance.html`、OG、JSON-LD 都用這個）。聯絡信箱 `rwei.studio@gmail.com` |
| 張育瑋 | 本人姓名（`index.html` 個人簡介、`resume.html`）。個人信箱 `ywzhang0913@gmail.com` |
| github `ywzhang13` | 程式碼帳號 / repo 擁有者 |

---

## 2. 技術棧

- 純 **HTML + 內嵌 CSS**，少量原生 JS。沒有 React/Next/Tailwind/打包工具。
- 字型走 Google Fonts CDN（**Outfit** + Noto Sans TC；2026-06-12 從 Poppins 升級為 Outfit）。
- CSS 設計語彙：`--r-card:16px`、`--r-pill:999px`（全站膠囊按鈕）、fluid `clamp()` 字級、shadow token、IntersectionObserver scroll-reveal。
- 技術 Logo 走 Simple Icons CDN（`https://cdn.simpleicons.org/{slug}/64748B`）。
- `package.json` 只有一個 devDependency（`@types/google.maps`）、`node_modules/` 與 `.next/` 是早期殘留，**對網站運作無作用**，可忽略或清掉。
- SEO 基建：`sitemap.xml`、`robots.txt`、頁內 JSON-LD（Schema.org）、Open Graph 卡片。

---

## 3. 目錄結構

```
portfolio-site/
├── freelance.html      # ★ 主力頁：R-Wei Studio 接案 landing（SEO 主頁，sitemap priority 1.0）
├── index.html          # 個人極簡名片頁（張育瑋 Developer，頭像+聯繫+GitHub）
├── resume.html         # 履歷頁（robots noindex，只給直接連結看，不被搜尋）
├── upload-helper.html  # 開發小工具：批次上傳截圖用，非對外頁
├── images/             # 63 個檔：六個作品的截圖/影片/OG 圖（og-rwei.png、profile.jpg…）
├── CNAME               # 自訂網域：rwei-studio.com（GitHub Pages 用）
├── sitemap.xml robots.txt   # 只收錄 / 與 /freelance.html
├── package.json package-lock.json node_modules/ .next/   # 殘留，無作用
└── .gitignore
```

### freelance.html 區塊（主頁）
`#services 服務項目` → `#value 不只是網站而是能營運的系統` → `#pricing 服務方案/參考報價` → `#skills 技術能力` → `#projects 作品案例` → `#why 為什麼選我` → `#process 合作流程` → `#faq 常見問題` → `#contact 聯絡`。手機版有漢堡選單。

### 作品案例(images/ 對應)
**Virtual Office AI**（首卡，AI 平台・自主產品；輪播 3 格＝voai-demo.mp4 影片自動播放 + voai-office.png + voai-tutorial.png；`freelance.html` 與 `resume.html` 兩頁都有，技術標籤用 **Phaser 4** 不是 3）、即時監控管理系統(claw-monitor)、揪旅 JiuTrip(旅行規劃+分帳)、新優生化 PIF 系統(化粧品產品資訊檔案)、沐居良品(台灣家具電商)、美食收藏家 Food Map AI、Together(地圖社交活動)、AI 業務助理(n8n 自動化)。

### 服務方案／報價（freelance.html，異動頻繁）
一頁式網站 NT$20,000 起、企業形象官網 60,000 起、基本電商 120,000 起（含多元支付；基本金流串接為加購）、AI 自動化／LINE Bot 50,000 起、客製系統／SaaS 報價制。
> 注意：報價與文案是最常改的部分（見 git log）。改價時記得同步 `freelance.html` 的 `#pricing`、`<meta description>`、`og:description` 三處，否則 SEO 摘要會與頁面不一致。

---

## 4. 怎麼啟動（本機預覽）

沒有建置流程，直接開檔或起個靜態伺服器即可：
```bash
cd ~/Documents/開發/portfolio-site
python3 -m http.server 8000   # 然後開 http://localhost:8000/freelance.html
# 或直接用瀏覽器打開 freelance.html
```

---

## 5. 怎麼部署

- 部署平台：**GitHub Pages**，repo `ywzhang13/portfolio-site`，分支 `main`。
- **push 到 `main` 即自動發佈**，無建置步驟。
- 自訂網域 `rwei-studio.com` 由根目錄 `CNAME` 綁定；SSL 由 GitHub Pages 自動簽發。
  （git log 有「unset → re-add custom domain 觸發重簽 SSL」的紀錄 —— 若憑證出問題，這是已驗證的救援手法。）
- 改完記得：新增頁面要一併更新 `sitemap.xml`；不想被搜尋的頁面加 `<meta name="robots" content="noindex, nofollow">`（`resume.html` 即如此）。

---

## 6. 目前完成度

**已上線且持續優化中。**
- `freelance.html` 2026-06-12 完成 **v2 大改版**：Outfit 字型、深色 Navy 色系、全站膠囊按鈕、fluid 字級、scroll-reveal 動畫、IntersectionObserver（含 prefers-reduced-motion 保護）、Simple Icons CDN 技術 logo、報價區改 3+2 格局、Virtual Office AI 作品首卡（輪播圖）。
- `index.html` 同步升級 Outfit 字型、膠囊按鈕、新增 "接案服務・R-Wei Studio →" 連結。
- `resume.html` 履歷頁完成（robots noindex）。
- 近期 commit 多在調報價與文案（電商 80k→120k、移除發票訴求、FAQ 製作時程、Hero 文案重定位、報價卡按鈕導向 #contact）。

---

## 7. 待辦與已知問題

這是小型靜態站，沒有嚴重技術債，以下為維護注意事項：
1. **殘留檔**：`package.json` / `node_modules/` / `.next/` 對網站無作用，可清掉以免誤導（清掉不影響部署）。
2. **報價三處同步**：改價只改 `#pricing` 區塊不夠，要連 `<meta description>` 與 `og:description` 一起改，否則 Google/社群分享摘要會顯示舊價。
3. **sitemap 只收兩頁**（`/`、`/freelance.html`）；若日後想讓更多頁被收錄要手動加。
4. `resume.html` 檔案權限是 `600`（僅本人可讀）——本機不影響，git 不追蹤權限，提醒別誤刪 noindex 標籤導致履歷被搜尋到。
5. 信箱兩套（接案 `rwei.studio@gmail.com` vs 個人 `ywzhang0913@gmail.com`）是刻意區分，改文案時別混用。
