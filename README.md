# Greeny-Search 🌿

**Greeny-Search** 是一個基於 Java 與 Spring Boot 開發的智慧搜尋引擎後端系統。它能透過 Google 進行網頁檢索，並結合自定義的關鍵字加權演算法與樹狀結構計分，為使用者提供更精準、更具相關性的搜尋結果排序。

## 🚀 核心功能

* **Google 搜尋整合**：透過 `GoogleQueryService` 模擬瀏覽器行為，抓取 Google 搜尋結果並自動解碼 URL。
* **自定義加權計分**：可設定多組關鍵字（如：環保、永續）及其權重，系統自動統計網頁中的關鍵字頻次。
* **樹狀結構演算**：
    * 利用 **Post-order ** 算法計算得分。
    * 子節點（關聯網頁）的分數會自動累加至父節點，實現階層式的網站價值評估。
* **自動排序系統**：搜尋結果依據計算出的總分進行降序排列，優先呈現最高價值的內容。

## 📁 檔案結構說明

| 檔案名稱 | 職責說明 |
| :--- | :--- |
| **GoogleSearchController.java** | RESTful API 進入點，處理前端 `/api/search` 請求。 |
| **GoogleQueryService.java** | 負責抓取 Google 網頁 HTML 並解析搜尋結果清單。 |
| **WebTree.java / WebNode.java** | 核心資料結構，負責建構網頁層級並執行後序計分演算。 |
| **WebPage.java** | 封裝網頁資訊（標題、URL）及計算單一頁面得分。 |
| **WordCounter.java** | 負責從目標網址下載內容並精確統計特定關鍵字出現次數。 |
| **Keyword.java** | 定義關鍵字物件及其權重值。 |

## 🛠️ 技術層

* **後端框架**: Spring Boot
* **解析工具**: [Jsoup](https://jsoup.org/) (用於解析 HTML 標籤)
* **開發語言**: Java 8+
* **通訊協議**: HTTP/HTTPS (URL & URLConnection)



## ⚖️ 計分邏輯
系統依據以下公式計算每個節點的基礎分：
$TotalScore = \sum (KeywordCount \times KeywordWeight)$

最終 `WebNode` 的分數會包含其自身分數加上所有子節點的總分。

---
