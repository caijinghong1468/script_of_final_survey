# NCCU Survey Auto-Filler (政大教學意見調查自動填寫)

這是一個簡單的 JavaScript 工具，用於輔助填寫國立政治大學的教學意見調查表。它能自動將大部分評分項目填寫為正向回饋，節省您的時間。

## 🚀 功能特色
- **自動評分**：將所有量表題自動勾選為「非常同意」或「提升 80~100%」。
- **修課狀態處理**：自動將「我沒有修習本課程」選為「否」（即確認有修課）。
- **預設感謝語**：在意見回饋欄位自動填入簡易感謝詞。
- **防止手殘**：自動勾選同意聲明，但保留最後送出按鈕由您親自確認。

## 📖 使用教學 (How to Use)

### 步驟 1：複製程式碼
複製以下完整的 JavaScript 程式碼：

```javascript
(function() {
    // Helper function to set radio button value
    function setRadio(name, val) {
        var radios = document.getElementsByName(name);
        if (!radios.length) return;
        
        let found = false;
        for(var i=0; i<radios.length; i++) {
            if(radios[i].value == val) {
                radios[i].checked = true;
                found = true;
            }
        }
        if (!found && radios.length > 0) {
            radios[0].checked = true;
        }
    }

    // 1. Learning Status (學習狀況)
    setRadio('S08', '1'); // 缺課情形: A.從未缺課
    setRadio('S09', '2'); // 預習時間: B.1小時
    setRadio('S10', '2'); // 複習時間: B.1小時

    // 2. Learning Outcomes (學習成果)
    setRadio('S13', '1'); // 清楚瞭解: A.非常同意
    setRadio('S14', '1'); // 運用知識: A.非常同意
    setRadio('S15', '1'); // 提升興趣: A.非常同意

    // 3. Teaching Effectiveness (教學成效)
    setRadio('S18', '1'); // 教學大綱: A.非常同意
    setRadio('S19', '1'); // 組織規劃: A.非常同意
    setRadio('S20', '1'); // 適切教材: A.非常同意
    setRadio('S21', '1'); // 有效學習: A.非常同意
    setRadio('S22', '1'); // 表達內容: A.非常同意

    // CRITICAL: S23 "I did NOT take this course" -> Must select "No" (2)
    setRadio('S23', '2'); // 6. 我沒有修習本課程: B.否 (代表有修習)

    setRadio('S24', '1'); // 評量公平: A.非常同意
    setRadio('S25', '1'); // 充分備課: A.非常同意
    setRadio('S26', '1'); // 鼓勵提問: A.非常同意
    setRadio('S27', '1'); // 認真負責: A.非常同意
    setRadio('S28', '1'); // 收穫良多: A.非常同意

    // 4. Feedback (意見回饋)
    var m31 = document.getElementsByName('M31');
    for(let i=0; i<Math.min(m31.length, 3); i++) m31[i].checked = true; // 勾選前三個優點

    var m32 = document.getElementsByName('M32'); // 建議改進: 不勾選 (表示滿意)
    
    // 文字意見
    var t33 = document.getElementsByName('T33');
    if(t33.length > 0) t33[0].value = "謝謝老師的指導，收穫很多！";

    // 5. Key Competencies (關鍵能力)
    ['S36', 'S37', 'S38', 'S39', 'S40', 'S41', 'S42'].forEach(name => {
        setRadio(name, '5'); // 80%~100% improvement
    });

    // 6. Agreement
    var agree = document.getElementsByName('agree');
    if(agree.length > 0) agree[0].checked = true;

    console.log("Form filled successfully!");
    alert("問卷已自動填寫完畢！\n\n檢查項目：\n1. S23 已選「否」（代表有修課）\n2. 若有「彈性授課」相關題目(S45等)可能需要手動補充。\n\n請確認內容後手動點擊「確認送出」。");
})();
```
### 步驟 2：進入任意課程教學意見調查
進入政大的教學意見調查頁面，確保畫面停留在你要填寫的那門課的問卷上。
### 步驟 3：打開「開發者工具」
1. 在網頁任意空白處按 滑鼠右鍵，選擇 「檢查」(Inspect)。 (注意：每次填不同課堂需重新開啟檢查頁面，否則程式會失效)
2. 在 主控台（Console） 的空白處點一下。
3. 貼上剛剛複製的程式碼，並按下 Enter 鍵。  
**（注意：如果是第一次貼上會出現警示訊息問你是否確定要貼上？你只需要照上面寫的文字輸入就可以了！）**
5. Enter後，網頁會跳出「問卷已自動填寫完畢」的提示視窗，就完成了。
---

## ⚠️ 免責聲明 (Disclaimer)

本程式僅提供輔助填寫功能，程式已有預設選項，如有需要不同選項，請自行更改程式，
**使用者須自行確認填寫內容符合真實意願**。

1. **內容責任**：腳本預設內容僅供參考（如「非常同意」），若您對該課程有不同意見，請務必手動修改後再送出。
2. **風險自負**：使用本工具所產生的任何結果（如問卷有效性疑慮），開發者不負任何責任。
3. **適用範圍**：本腳本針對特定時期的問卷 HTML 結構編寫，若學校更新問卷系統，腳本可能會失效。

---
*Created for NCCU Students.*
