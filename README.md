# 🤖 Discord: Last Meadow Online - Auto Bot 🌾

![Last Meadow Online](https://img.shields.io/badge/Discord-Last_Meadow_Online-5865F2?style=for-the-badge&logo=discord&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

An automated script (Auto Bot) for the **Last Meadow Online** (April Fools' Day Event) on Discord. It helps you farm resources automatically with a super easy-to-use floating UI control panel! 

> 🌍 **Bilingual Support:** The script automatically detects and works with both **English** and **Thai** Discord interfaces.

---

### 📖 Choose your language / เลือกภาษา
* [🇺🇸 English Documentation](#-english-version)
* [🇹🇭 คู่มือการใช้งานภาษาไทย](#-เวอร์ชันภาษาไทย-thai-version)
* [💻 The Script / โค้ดสคริปต์](#-the-script--โค้ดสคริปต์)

---

## 🇺🇸 English Version

### ✨ Features
* ⚔️ **Adventure Mode:** Auto-Clicker that clicks rapidly for you.
* 🛠️ **Craft Mode:** Automatically plays the arrow-key mini-game (includes a 40ms delay per key press to make it look natural and prevent game glitches).
* 🎯 **Combat Mode:** Auto-Aim system that instantly clicks the target as soon as it appears.
* 📦 **Auto-Claim & Error Handling:** * Automatically clicks **"Continue"** to claim rewards.
    * Automatically clicks **"Back"** when the "Out of resources" server warning pops up so the loop doesn't break.
* 🎛️ **Floating Control Panel:** A floating UI on the top right corner. You can toggle each mode ON/OFF independently, or run all 3 modes simultaneously.

### 🚀 How to Use
1. Open Discord on your web browser (or the desktop app with Developer Mode enabled).
2. Go to the **Last Meadow Online** mini-game window.
3. Press `F12` or `Ctrl + Shift + I` on your keyboard to open **Developer Tools**.
4. Go to the **Console** tab. *(Note: If this is your first time using the console, Discord might block pasting. Type `allow pasting` and press Enter first.)*
5. Copy the script from the **[The Script](#-the-script--โค้ดสคริปต์)** section below, paste it into the Console, and press `Enter`.
6. The **🤖 LM Auto Bot** control panel will appear in the top right corner. You're ready to go!

---

## 🇹🇭 เวอร์ชันภาษาไทย (Thai Version)

### ✨ ฟีเจอร์หลัก
* ⚔️ **โหมดผจญภัย (Adventure):** ระบบ Auto-Clicker คลิกรัวๆ อัตโนมัติ
* 🛠️ **โหมดสร้าง (Craft):** เล่นมินิเกมกดลูกศรอัตโนมัติ (มีระบบหน่วงเวลา 40ms ต่อปุ่ม เพื่อความเนียนและป้องกันเกมรวน)
* 🎯 **โหมดต่อสู้ (Combat):** ระบบ Auto-Aim เล็งและคลิกเป้าหมายอัตโนมัติทันทีที่ปรากฏ
* 📦 **Auto-Claim & Error Handling:** * กดปุ่ม **"ไปต่อ"** เพื่อรับของรางวัลอัตโนมัติ
    * กดปุ่ม **"กลับ"** ให้อัตโนมัติเมื่อเจอหน้าต่างแจ้งเตือนเซิร์ฟเวอร์ทรัพยากรหมด (Out of resources)
* 🎛️ **Floating Control Panel:** แผงควบคุม UI ลอยตัวมุมขวาบน สามารถกดสลับ เปิด-ปิด (ON/OFF) แต่ละโหมดแยกกันได้อย่างอิสระ หรือจะรันพร้อมกัน 3 โหมดเลยก็ได้!

### 🚀 วิธีใช้งาน
1. เปิด Discord บนเว็บเบราว์เซอร์ (หรือแอปพลิเคชันที่เปิดโหมดนักพัฒนาไว้)
2. เข้าไปที่หน้าต่างมินิเกม **Last Meadow Online**
3. กดปุ่ม `F12` หรือ `Ctrl + Shift + I` บนคีย์บอร์ด เพื่อเปิดหน้าต่าง **Developer Tools**
4. ไปที่แท็บ **Console** *(หมายเหตุ: หากเป็นการเปิด Console ครั้งแรก ระบบอาจไม่อนุญาตให้วางโค้ด คุณต้องพิมพ์คำว่า `allow pasting` ลงไปแล้วกด Enter ก่อน 1 ครั้ง)*
5. คัดลอกโค้ดสคริปต์จากหัวข้อ **[โค้ดสคริปต์](#-the-script--โค้ดสคริปต์)** ด้านล่างนี้ไปวางในช่อง Console แล้วกด `Enter`
6. แผงควบคุม **🤖 LM Auto Bot** จะปรากฏขึ้นที่มุมขวาบนของหน้าจอ พร้อมลุย!

---

## 💻 The Script / โค้ดสคริปต์

```javascript
// Prevent duplicate panels / ป้องกันการสร้าง Pop-up ซ้ำ
if (document.getElementById('lm-bot-panel')) {
    document.getElementById('lm-bot-panel').remove();
}

let intervals = { adventure: null, craft: null, combat: null };
let isCrafting = false; 

// ==========================================
// Helper: Find and click button by text (Bilingual)
// ==========================================
function clickPopupByText(textArray) {
    for (let text of textArray) {
        let xpath = `//*[text()='${text}']`;
        let element = document.evaluate(xpath, document, null, XPathResult.FIRST_ORDERED_NODE_TYPE, null).singleNodeValue;
        if (element) {
            let btn = element.closest('[role="button"]') || element.closest('.clickable__5c90e') || element;
            btn.click();
            return true; 
        }
    }
    return false;
}

// ==========================================
// 1. Adventure Mode
// ==========================================
function toggleAdventure(btnElement) {
    if (intervals.adventure) {
        clearInterval(intervals.adventure);
        intervals.adventure = null;
        btnElement.style.background = '#ED4245'; 
        btnElement.innerText = 'Adventure: OFF';
    } else {
        btnElement.style.background = '#57F287'; 
        btnElement.innerText = 'Adventure: ON';
        intervals.adventure = setInterval(() => {
            if (clickPopupByText(['กลับ', 'Back'])) return;

            const texts = document.querySelectorAll('.visibleText__65fca');
            texts.forEach(text => {
                if (['ผจญภัย', 'Adventure'].includes(text.textContent)) {
                    let btn = text.closest('.clickable__5c90e');
                    if (btn && !btn.classList.contains('disabled__65fca')) btn.click();
                }
            });
        }, 50); 
    }
}

// ==========================================
// 2. Craft Mode 
// ==========================================
function toggleCraft(btnElement) {
    if (intervals.craft) {
        clearInterval(intervals.craft);
        intervals.craft = null;
        btnElement.style.background = '#ED4245';
        btnElement.innerText = 'Craft: OFF';
    } else {
        btnElement.style.background = '#57F287';
        btnElement.innerText = 'Craft: ON';
        
        intervals.craft = setInterval(async () => {
            if (isCrafting) return;
            if (clickPopupByText(['ไปต่อ', 'Continue'])) return;
            if (clickPopupByText(['กลับ', 'Back'])) return;

            const sequenceContainer = document.querySelector('.sequences__34527');
            if (sequenceContainer) {
                isCrafting = true;
                const arrows = sequenceContainer.querySelectorAll('img');
                
                for (let img of arrows) {
                    const keyName = img.getAttribute('alt'); 
                    if (keyName) {
                        document.dispatchEvent(new KeyboardEvent('keydown', { key: keyName, code: keyName, bubbles: true }));
                        document.dispatchEvent(new KeyboardEvent('keyup', { key: keyName, code: keyName, bubbles: true }));
                        await new Promise(r => setTimeout(r, 40)); 
                    }
                }
                await new Promise(r => setTimeout(r, 500)); 
                isCrafting = false;
                return; 
            }

            const texts = document.querySelectorAll('.visibleText__65fca');
            texts.forEach(text => {
                if (['สร้าง', 'Craft'].includes(text.textContent)) {
                    let btn = text.closest('.clickable__5c90e');
                    if (btn && !btn.classList.contains('disabled__65fca')) btn.click();
                }
            });
        }, 200); 
    }
}

// ==========================================
// 3. Combat Mode
// ==========================================
function toggleCombat(btnElement) {
    if (intervals.combat) {
        clearInterval(intervals.combat);
        intervals.combat = null;
        btnElement.style.background = '#ED4245';
        btnElement.innerText = 'Combat: OFF';
    } else {
        btnElement.style.background = '#57F287';
        btnElement.innerText = 'Combat: ON';
        
        intervals.combat = setInterval(() => {
            if (clickPopupByText(['ไปต่อ', 'Continue'])) return;
            if (clickPopupByText(['กลับ', 'Back'])) return;

            let targetImg = document.querySelector('img[alt="target"]');
            if (targetImg) {
                let targetBtn = targetImg.closest('.clickable__5c90e') || targetImg;
                targetBtn.click();
                return;
            }

            const texts = document.querySelectorAll('.visibleText__65fca');
            texts.forEach(text => {
                if (['การต่อสู้', 'Combat', 'Battle'].includes(text.textContent)) {
                    let btn = text.closest('.clickable__5c90e');
                    if (btn && !btn.classList.contains('disabled__65fca')) btn.click();
                }
            });
        }, 100); 
    }
}

// ==========================================
// Kill Switch
// ==========================================
function killBot() {
    clearInterval(intervals.adventure);
    clearInterval(intervals.craft);
    clearInterval(intervals.combat);
    document.getElementById('lm-bot-panel').remove();
    console.log("Bot Stopped & Removed");
}

// ==========================================
// Build UI Panel
// ==========================================
const panel = document.createElement('div');
panel.id = 'lm-bot-panel';
panel.style.cssText = `
    position: fixed; top: 20px; right: 20px; width: 200px;
    background: #2b2d31; border: 2px solid #5865F2; border-radius: 8px;
    padding: 15px; z-index: 999999; font-family: 'gg sans', sans-serif;
    color: white; box-shadow: 0 8px 16px rgba(0,0,0,0.5);
    display: flex; flex-direction: column; gap: 10px;
`;

const title = document.createElement('div');
title.innerText = '🤖 LM Auto Bot';
title.style.cssText = 'font-weight: bold; text-align: center; margin-bottom: 5px; font-size: 16px; border-bottom: 1px solid #4e5058; padding-bottom: 8px;';
panel.appendChild(title);

function createBtn(text, onClickHandler, color = '#ED4245') {
    const btn = document.createElement('button');
    btn.innerText = text;
    btn.style.cssText = `
        background: ${color}; color: white; border: none; padding: 8px;
        border-radius: 4px; cursor: pointer; font-weight: bold; transition: 0.2s;
    `;
    btn.onclick = () => onClickHandler(btn);
    return btn;
}

panel.appendChild(createBtn('Adventure: OFF', toggleAdventure));
panel.appendChild(createBtn('Craft: OFF', toggleCraft));
panel.appendChild(createBtn('Combat: OFF', toggleCombat));

const closeBtn = createBtn('❌ Close Bot', killBot, '#5865F2');
closeBtn.style.marginTop = '10px';
panel.appendChild(closeBtn);

document.body.appendChild(panel);
