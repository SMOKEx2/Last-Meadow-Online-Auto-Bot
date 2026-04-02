# 🤖 Discord: Last Meadow Online - Auto Bot 🌾

สคริปต์ Auto Bot สำหรับกิจกรรม **Last Meadow Online** (April Fools' Day Event) บน Discord ช่วยคุณฟาร์มทรัพยากรแบบอัตโนมัติครบจบในสคริปต์เดียว พร้อมแผงควบคุม UI ลอยตัวที่ใช้งานง่ายสุดๆ!

![Last Meadow Online](https://img.shields.io/badge/Discord-Last_Meadow_Online-5865F2?style=for-the-badge&logo=discord&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

---

## ✨ ฟีเจอร์หลัก (Features)

* ⚔️ **โหมดผจญภัย (Adventure):** ระบบ Auto-Clicker คลิกรัวๆ อัตโนมัติ
* 🛠️ **โหมดสร้าง (Craft):** เล่นมินิเกมกดลูกศรอัตโนมัติ (มีระบบหน่วงเวลา 40ms ต่อปุ่ม เพื่อความเนียนและป้องกันเกมรวน)
* 🎯 **โหมดต่อสู้ (Combat):** ระบบ Auto-Aim เล็งและคลิกเป้าหมายอัตโนมัติทันทีที่ปรากฏ
* 📦 **Auto-Claim & Error Handling:** * กดปุ่ม **"ไปต่อ"** เพื่อรับของรางวัลอัตโนมัติ
    * กดปุ่ม **"กลับ"** ให้อัตโนมัติเมื่อเจอหน้าต่างแจ้งเตือนเซิร์ฟเวอร์ทรัพยากรหมด (Out of resources)
* 🎛️ **Floating Control Panel:** แผงควบคุม UI ลอยตัวมุมขวาบน สามารถกดสลับ เปิด-ปิด (ON/OFF) แต่ละโหมดแยกกันได้อย่างอิสระ หรือจะรันพร้อมกัน 3 โหมดเลยก็ได้!

---

## 🚀 วิธีใช้งาน (How to Use)

1. เปิด Discord บนเว็บเบราว์เซอร์ (หรือแอปพลิเคชันที่เปิดโหมดนักพัฒนาไว้)
2. เข้าไปที่หน้าต่างมินิเกม **Last Meadow Online**
3. กดปุ่ม `F12` หรือ `Ctrl + Shift + I` บนคีย์บอร์ด เพื่อเปิดหน้าต่าง **Developer Tools**
4. ไปที่แท็บ **Console** > ⚠️ *หมายเหตุ: หากเป็นการเปิด Console ครั้งแรก ระบบอาจไม่อนุญาตให้วางโค้ด คุณต้องพิมพ์คำว่า `allow pasting` ลงไปแล้วกด Enter ก่อน 1 ครั้ง*
5. คัดลอกโค้ดสคริปต์ด้านล่างนี้ไปวางในช่อง Console แล้วกด `Enter`
6. แผงควบคุม **🤖 LM Auto Bot** จะปรากฏขึ้นที่มุมขวาบนของหน้าจอ พร้อมลุย!

---

## 💻 โค้ดสคริปต์ (The Script)

```javascript
// ป้องกันการสร้าง Pop-up ซ้ำ
if (document.getElementById('lm-bot-panel')) {
    document.getElementById('lm-bot-panel').remove();
}

let intervals = { adventure: null, craft: null, combat: null };
let isCrafting = false; 

// ==========================================
// ฟังก์ชันช่วย: ค้นหาและกดปุ่มจากข้อความบนจอ
// ==========================================
function clickPopupByText(text) {
    let xpath = `//*[text()='${text}']`;
    let element = document.evaluate(xpath, document, null, XPathResult.FIRST_ORDERED_NODE_TYPE, null).singleNodeValue;
    if (element) {
        let btn = element.closest('[role="button"]') || element.closest('.clickable__5c90e') || element;
        btn.click();
        return true; 
    }
    return false;
}

// ==========================================
// 1. โหมดผจญภัย
// ==========================================
function toggleAdventure(btnElement) {
    if (intervals.adventure) {
        clearInterval(intervals.adventure);
        intervals.adventure = null;
        btnElement.style.background = '#ED4245'; 
        btnElement.innerText = 'ผจญภัย: OFF';
    } else {
        btnElement.style.background = '#57F287'; 
        btnElement.innerText = 'ผจญภัย: ON';
        intervals.adventure = setInterval(() => {
            if (clickPopupByText('กลับ')) return;

            const texts = document.querySelectorAll('.visibleText__65fca');
            texts.forEach(text => {
                if (text.textContent === 'ผจญภัย') {
                    let btn = text.closest('.clickable__5c90e');
                    if (btn && !btn.classList.contains('disabled__65fca')) btn.click();
                }
            });
        }, 50); 
    }
}

// ==========================================
// 2. โหมดสร้าง 
// ==========================================
function toggleCraft(btnElement) {
    if (intervals.craft) {
        clearInterval(intervals.craft);
        intervals.craft = null;
        btnElement.style.background = '#ED4245';
        btnElement.innerText = 'สร้าง: OFF';
    } else {
        btnElement.style.background = '#57F287';
        btnElement.innerText = 'สร้าง: ON';
        
        intervals.craft = setInterval(async () => {
            if (isCrafting) return;
            if (clickPopupByText('ไปต่อ')) return;
            if (clickPopupByText('กลับ')) return;

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
                if (text.textContent === 'สร้าง') {
                    let btn = text.closest('.clickable__5c90e');
                    if (btn && !btn.classList.contains('disabled__65fca')) btn.click();
                }
            });
        }, 200); 
    }
}

// ==========================================
// 3. โหมดต่อสู้
// ==========================================
function toggleCombat(btnElement) {
    if (intervals.combat) {
        clearInterval(intervals.combat);
        intervals.combat = null;
        btnElement.style.background = '#ED4245';
        btnElement.innerText = 'ต่อสู้: OFF';
    } else {
        btnElement.style.background = '#57F287';
        btnElement.innerText = 'ต่อสู้: ON';
        
        intervals.combat = setInterval(() => {
            if (clickPopupByText('ไปต่อ')) return;
            if (clickPopupByText('กลับ')) return;

            let targetImg = document.querySelector('img[alt="target"]');
            if (targetImg) {
                let targetBtn = targetImg.closest('.clickable__5c90e') || targetImg;
                targetBtn.click();
                return;
            }

            const texts = document.querySelectorAll('.visibleText__65fca');
            texts.forEach(text => {
                if (text.textContent === 'การต่อสู้') {
                    let btn = text.closest('.clickable__5c90e');
                    if (btn && !btn.classList.contains('disabled__65fca')) btn.click();
                }
            });
        }, 100); 
    }
}

// ==========================================
// ระบบปิดบอททั้งหมด
// ==========================================
function killBot() {
    clearInterval(intervals.adventure);
    clearInterval(intervals.craft);
    clearInterval(intervals.combat);
    document.getElementById('lm-bot-panel').remove();
    console.log("Bot Stopped & Removed");
}

// ==========================================
// สร้าง UI Panel
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

panel.appendChild(createBtn('ผจญภัย: OFF', toggleAdventure));
panel.appendChild(createBtn('สร้าง: OFF', toggleCraft));
panel.appendChild(createBtn('ต่อสู้: OFF', toggleCombat));

const closeBtn = createBtn('❌ ปิดบอททั้งหมด', killBot, '#5865F2');
closeBtn.style.marginTop = '10px';
panel.appendChild(closeBtn);

document.body.appendChild(panel);
