# 🤖 Discord: Last Meadow Online - Auto Bot 🌾

![Last Meadow Online](https://img.shields.io/badge/Discord-Last_Meadow_Online-5865F2?style=for-the-badge&logo=discord&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

An automated script (Auto Bot) for the **Last Meadow Online** (April Fools' Day Event) on Discord. It helps you farm resources automatically with a modern, glassmorphism floating UI! 

> 🌍 **Bilingual & Modern UI:** Features a sleek dark-mode panel with an interactive EN/TH language toggle button built right into the interface!

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
* 🎛️ **Floating Control Panel:** A glassmorphism UI on the top right corner. You can toggle each mode ON/OFF independently, or run all 3 modes simultaneously!

### 🚀 How to Use
1. Open Discord on your web browser (or the desktop app with Developer Mode enabled).
2. Go to the **Last Meadow Online** mini-game window.
3. Press `F12` or `Ctrl + Shift + I` on your keyboard to open **Developer Tools**.
4. Go to the **Console** tab. *(Note: If this is your first time using the console, Discord might block pasting. Type `allow pasting` and press Enter first.)*
5. Copy the script from the **[The Script](#-the-script--โค้ดสคริปต์)** section below, paste it into the Console, and press `Enter`.
6. The **🤖 LM Auto Bot** control panel will appear. You're ready to go!

---

## 🇹🇭 เวอร์ชันภาษาไทย (Thai Version)

### ✨ ฟีเจอร์หลัก
* ⚔️ **โหมดผจญภัย (Adventure):** ระบบ Auto-Clicker คลิกรัวๆ อัตโนมัติ
* 🛠️ **โหมดสร้าง (Craft):** เล่นมินิเกมกดลูกศรอัตโนมัติ (หน่วงเวลา 40ms ต่อปุ่ม เพื่อความเนียนและป้องกันเกมรวน)
* 🎯 **โหมดต่อสู้ (Combat):** ระบบ Auto-Aim เล็งและคลิกเป้าหมายอัตโนมัติทันทีที่ปรากฏ
* 📦 **Auto-Claim & Error Handling:** * กดปุ่ม **"ไปต่อ"** เพื่อรับของรางวัลอัตโนมัติ
    * กดปุ่ม **"กลับ"** ให้อัตโนมัติเมื่อเจอหน้าต่างแจ้งเตือนเซิร์ฟเวอร์ทรัพยากรหมด
* 🎛️ **Floating Control Panel:** แผงควบคุมดีไซน์กระจกใส สามารถกดสลับ เปิด-ปิด (ON/OFF) และเปลี่ยนภาษาได้ทันที

### 🚀 วิธีใช้งาน
1. เปิด Discord บนเว็บเบราว์เซอร์ (หรือแอปพลิเคชันที่เปิดโหมดนักพัฒนาไว้)
2. เข้าไปที่หน้าต่างมินิเกม **Last Meadow Online**
3. กดปุ่ม `F12` หรือ `Ctrl + Shift + I` บนคีย์บอร์ด เพื่อเปิดหน้าต่าง **Developer Tools**
4. ไปที่แท็บ **Console** *(หมายเหตุ: หากเพิ่งเคยเปิด Console ระบบอาจบล็อกไม่ให้วางโค้ด ต้องพิมพ์ `allow pasting` แล้วกด Enter ก่อน 1 ครั้ง)*
5. คัดลอกโค้ดสคริปต์จากหัวข้อ **[โค้ดสคริปต์](#-the-script--โค้ดสคริปต์)** ด้านล่างนี้ไปวางในช่อง Console แล้วกด `Enter`
6. แผงควบคุม **🤖 LM Auto Bot** จะปรากฏขึ้น พร้อมฟาร์มทันที!

---

## 💻 The Script / โค้ดสคริปต์

คัดลอกโค้ดด้านล่างนี้ไปวางใน **Console** ของบราวเซอร์ (F12) ได้เลยครับ / Copy and paste the code below into your browser's **Console** (F12).

```javascript
// ==========================================
// 🧹 CLEANUP & INITIALIZATION
// ==========================================
if (document.getElementById('lm-bot-panel')) document.getElementById('lm-bot-panel').remove();
if (document.getElementById('lm-bot-styles')) document.getElementById('lm-bot-styles').remove();

let intervals = { adventure: null, craft: null, combat: null };
let isCrafting = false; 
let currentLang = 'th'; // Default language

// ==========================================
// 🌍 TRANSLATION DICTIONARY
// ==========================================
const textData = {
    th: { title: '🤖 LM Auto Bot', adv: 'ผจญภัย', craft: 'สร้าง', combat: 'ต่อสู้', close: '❌ ปิดบอททั้งหมด', on: 'ON', off: 'OFF' },
    en: { title: '🤖 LM Auto Bot', adv: 'Adventure', craft: 'Craft', combat: 'Combat', close: '❌ Close Bot', on: 'ON', off: 'OFF' }
};

// ==========================================
// 🎨 MODERN CSS INJECTION
// ==========================================
const styles = document.createElement('style');
styles.id = 'lm-bot-styles';
styles.innerHTML = `
    #lm-bot-panel {
        position: fixed; top: 24px; right: 24px; width: 220px;
        background: rgba(30, 31, 34, 0.85);
        backdrop-filter: blur(10px); -webkit-backdrop-filter: blur(10px);
        border: 1px solid rgba(255, 255, 255, 0.1);
        border-radius: 12px; padding: 16px; z-index: 999999;
        font-family: 'gg sans', 'Helvetica Neue', sans-serif;
        color: white; box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        display: flex; flex-direction: column; gap: 10px;
        transition: all 0.3s ease;
    }
    .lm-header {
        display: flex; justify-content: space-between; align-items: center;
        border-bottom: 1px solid rgba(255,255,255,0.1); padding-bottom: 10px; margin-bottom: 5px;
    }
    .lm-title { font-weight: 800; font-size: 15px; text-shadow: 0 2px 4px rgba(0,0,0,0.3); }
    .lm-lang-btn {
        background: #4e5058; color: white; border: none; border-radius: 4px;
        padding: 4px 8px; font-size: 12px; font-weight: bold; cursor: pointer;
        transition: 0.2s;
    }
    .lm-lang-btn:hover { background: #6d6f78; transform: scale(1.05); }
    
    .lm-btn {
        border: none; padding: 10px; border-radius: 6px; color: white;
        font-weight: bold; font-size: 14px; cursor: pointer; transition: 0.2s;
        text-shadow: 0 1px 2px rgba(0,0,0,0.3);
        display: flex; justify-content: space-between; align-items: center;
    }
    .lm-btn:hover { filter: brightness(1.15); transform: translateY(-1px); }
    .lm-btn:active { transform: translateY(1px); filter: brightness(0.9); }
    
    .btn-off { background: #ED4245; box-shadow: 0 4px 0 #c93638; }
    .btn-off:active { box-shadow: 0 2px 0 #c93638; }
    .btn-on { background: #57F287; box-shadow: 0 4px 0 #46c46e; color: #000; text-shadow: none; }
    .btn-on:active { box-shadow: 0 2px 0 #46c46e; }
    .btn-close { background: transparent; border: 1px solid #ED4245; color: #ED4245; margin-top: 5px; justify-content: center;}
    .btn-close:hover { background: rgba(237, 66, 69, 0.1); }
`;
document.head.appendChild(styles);

// ==========================================
// ⚙️ CORE BOT LOGIC
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

function updateBtnUI(btn, modeKey, isRunning) {
    let t = textData[currentLang];
    btn.className = `lm-btn ${isRunning ? 'btn-on' : 'btn-off'}`;
    btn.innerHTML = `<span>${t[modeKey]}</span> <span>${isRunning ? t.on : t.off}</span>`;
}

function toggleAdventure(btnElement) {
    if (intervals.adventure) {
        clearInterval(intervals.adventure); intervals.adventure = null;
        updateBtnUI(btnElement, 'adv', false);
    } else {
        updateBtnUI(btnElement, 'adv', true);
        intervals.adventure = setInterval(() => {
            if (clickPopupByText(['กลับ', 'Back'])) return;
            document.querySelectorAll('.visibleText__65fca').forEach(text => {
                if (['ผจญภัย', 'Adventure'].includes(text.textContent)) {
                    let b = text.closest('.clickable__5c90e');
                    if (b && !b.classList.contains('disabled__65fca')) b.click();
                }
            });
        }, 50); 
    }
}

function toggleCraft(btnElement) {
    if (intervals.craft) {
        clearInterval(intervals.craft); intervals.craft = null;
        updateBtnUI(btnElement, 'craft', false);
    } else {
        updateBtnUI(btnElement, 'craft', true);
        intervals.craft = setInterval(async () => {
            if (isCrafting) return;
            if (clickPopupByText(['ไปต่อ', 'Continue', 'กลับ', 'Back'])) return;

            const seq = document.querySelector('.sequences__34527');
            if (seq) {
                isCrafting = true;
                for (let img of seq.querySelectorAll('img')) {
                    const key = img.getAttribute('alt'); 
                    if (key) {
                        document.dispatchEvent(new KeyboardEvent('keydown', { key, code: key, bubbles: true }));
                        document.dispatchEvent(new KeyboardEvent('keyup', { key, code: key, bubbles: true }));
                        await new Promise(r => setTimeout(r, 40)); 
                    }
                }
                await new Promise(r => setTimeout(r, 500)); 
                isCrafting = false; return; 
            }
            document.querySelectorAll('.visibleText__65fca').forEach(text => {
                if (['สร้าง', 'Craft'].includes(text.textContent)) {
                    let b = text.closest('.clickable__5c90e');
                    if (b && !b.classList.contains('disabled__65fca')) b.click();
                }
            });
        }, 200); 
    }
}

function toggleCombat(btnElement) {
    if (intervals.combat) {
        clearInterval(intervals.combat); intervals.combat = null;
        updateBtnUI(btnElement, 'combat', false);
    } else {
        updateBtnUI(btnElement, 'combat', true);
        intervals.combat = setInterval(() => {
            if (clickPopupByText(['ไปต่อ', 'Continue', 'กลับ', 'Back'])) return;
            
            let targetImg = document.querySelector('img[alt="target"]');
            if (targetImg) {
                (targetImg.closest('.clickable__5c90e') || targetImg).click(); return;
            }
            document.querySelectorAll('.visibleText__65fca').forEach(text => {
                if (['การต่อสู้', 'Combat', 'Battle'].includes(text.textContent)) {
                    let b = text.closest('.clickable__5c90e');
                    if (b && !b.classList.contains('disabled__65fca')) b.click();
                }
            });
        }, 100); 
    }
}

// ==========================================
// 🏗️ BUILD UI ELEMENTS
// ==========================================
const panel = document.createElement('div');
panel.id = 'lm-bot-panel';

const header = document.createElement('div');
header.className = 'lm-header';

const title = document.createElement('div');
title.className = 'lm-title';
title.innerText = textData[currentLang].title;

const langBtn = document.createElement('button');
langBtn.className = 'lm-lang-btn';
langBtn.innerText = '🇹🇭 TH';

// ปุ่มต่างๆ
const btnAdv = document.createElement('button');
const btnCraft = document.createElement('button');
const btnCombat = document.createElement('button');
const btnClose = document.createElement('button');

// อัปเดตข้อความทั้งหมดตามภาษา
function refreshLanguageUI() {
    title.innerText = textData[currentLang].title;
    langBtn.innerText = currentLang === 'th' ? '🇹🇭 TH' : '🇺🇸 EN';
    updateBtnUI(btnAdv, 'adv', !!intervals.adventure);
    updateBtnUI(btnCraft, 'craft', !!intervals.craft);
    updateBtnUI(btnCombat, 'combat', !!intervals.combat);
    btnClose.innerText = textData[currentLang].close;
}

// ระบบสลับภาษา
langBtn.onclick = () => {
    currentLang = currentLang === 'th' ? 'en' : 'th';
    refreshLanguageUI();
};

btnAdv.onclick = () => toggleAdventure(btnAdv);
btnCraft.onclick = () => toggleCraft(btnCraft);
btnCombat.onclick = () => toggleCombat(btnCombat);

btnClose.className = 'lm-btn btn-close';
btnClose.onclick = () => {
    clearInterval(intervals.adventure); clearInterval(intervals.craft); clearInterval(intervals.combat);
    panel.remove(); styles.remove(); console.log("Bot Stopped & Removed");
};

// นำประกอบเข้าด้วยกัน
header.appendChild(title);
header.appendChild(langBtn);
panel.appendChild(header);
panel.appendChild(btnAdv);
panel.appendChild(btnCraft);
panel.appendChild(btnCombat);
panel.appendChild(btnClose);

document.body.appendChild(panel);

// ตั้งค่า UI เริ่มต้น
refreshLanguageUI();
```

---

## ⚠️ Disclaimer / ข้อควรระวัง
**[EN]** This project is for educational purposes only. Using automated scripts, bots, or macros on Discord may violate their Terms of Service. Use at your own risk. The developer is not responsible for any bans, penalties, or consequences that may occur to your account.

**[TH]** โปรเจกต์นี้จัดทำขึ้นเพื่อการศึกษาเท่านั้น การใช้สคริปต์อัตโนมัติ (Bot/Macro) บนแพลตฟอร์ม Discord อาจขัดต่อเงื่อนไขการให้บริการ (Terms of Service) ผู้ใช้งานควรใช้งานด้วยความระมัดระวัง ผู้พัฒนาจะไม่รับผิดชอบต่อผลกระทบใดๆ ที่เกิดขึ้นกับบัญชีผู้ใช้ของคุณ

---
*Created with ❤️ by [ใส่ชื่อหรือ GitHub Username ของคุณที่นี่]*
