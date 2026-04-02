# 🤖 Discord: Last Meadow Online - Auto Bot 🌾

![Last Meadow Online](https://img.shields.io/badge/Discord-Last_Meadow_Online-5865F2?style=for-the-badge&logo=discord&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

An automated script (Auto Bot) for the **Last Meadow Online** (April Fools' Day Event) on Discord. It helps you farm resources automatically with a modern, glassmorphism floating UI! 

> 🌍 **Bilingual & Modern UI:** Features a sleek dark-mode panel with an interactive EN/TH language toggle button built right into the interface!

---

### 📖 Choose your language / เลือกภาษา
* [US English Documentation](#-english-version)
* [TH คู่มือการใช้งานภาษาไทย](#-เวอร์ชันภาษาไทย-thai-version)
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
if(document.getElementById("lm-bot-panel"))document.getElementById("lm-bot-panel").remove();if(document.getElementById("lm-bot-styles"))document.getElementById("lm-bot-styles").remove();let iv={a:null,c:null,cb:null},isC=!1,lng="th";const txt={th:{t:"🤖 LM Auto Bot",a:"ผจญภัย",c:"สร้าง",cb:"ต่อสู้",x:"❌ ปิดบอททั้งหมด",on:"ON",off:"OFF"},en:{t:"🤖 LM Auto Bot",a:"Adventure",c:"Craft",cb:"Combat",x:"❌ Close Bot",on:"ON",off:"OFF"}},st=document.createElement("style");st.id="lm-bot-styles",st.innerHTML=`#lm-bot-panel{position:fixed;top:24px;right:24px;width:220px;background:rgba(30,31,34,.85);backdrop-filter:blur(10px);-webkit-backdrop-filter:blur(10px);border:1px solid rgba(255,255,255,.1);border-radius:12px;padding:16px;z-index:999999;font-family:'gg sans',sans-serif;color:#fff;box-shadow:0 10px 30px rgba(0,0,0,.5);display:flex;flex-direction:column;gap:10px;transition:all .3s ease}.lm-header{display:flex;justify-content:space-between;align-items:center;border-bottom:1px solid rgba(255,255,255,.1);padding-bottom:10px;margin-bottom:5px}.lm-title{font-weight:800;font-size:15px;text-shadow:0 2px 4px rgba(0,0,0,.3)}.lm-lang-btn{background:#4e5058;color:#fff;border:none;border-radius:4px;padding:4px 8px;font-size:12px;font-weight:700;cursor:pointer;transition:.2s}.lm-lang-btn:hover{background:#6d6f78;transform:scale(1.05)}.lm-btn{border:none;padding:10px;border-radius:6px;color:#fff;font-weight:700;font-size:14px;cursor:pointer;transition:.2s;text-shadow:0 1px 2px rgba(0,0,0,.3);display:flex;justify-content:space-between;align-items:center}.lm-btn:hover{filter:brightness(1.15);transform:translateY(-1px)}.lm-btn:active{transform:translateY(1px);filter:brightness(.9)}.btn-off{background:#ED4245;box-shadow:0 4px 0 #c93638}.btn-off:active{box-shadow:0 2px 0 #c93638}.btn-on{background:#57F287;box-shadow:0 4px 0 #46c46e;color:#000;text-shadow:none}.btn-on:active{box-shadow:0 2px 0 #46c46e}.btn-close{background:0 0;border:1px solid #ED4245;color:#ED4245;margin-top:5px;justify-content:center}.btn-close:hover{background:rgba(237,66,69,.1)}`,document.head.appendChild(st);function clk(e){for(let t of e){let l=document.evaluate(`//*[text()='${t}']`,document,null,XPathResult.FIRST_ORDERED_NODE_TYPE,null).singleNodeValue;if(l)return(l.closest('[role="button"]')||l.closest(".clickable__5c90e")||l).click(),!0}return!1}function upd(e,t,l){let n=txt[lng];e.className=`lm-btn ${l?"btn-on":"btn-off"}`,e.innerHTML=`<span>${n[t]}</span> <span>${l?n.on:n.off}</span>`}function tA(e){iv.a?(clearInterval(iv.a),iv.a=null,upd(e,"a",!1)):(upd(e,"a",!0),iv.a=setInterval(()=>{clk(["กลับ","Back"])||document.querySelectorAll(".visibleText__65fca").forEach(e=>{if(["ผจญภัย","Adventure"].includes(e.textContent)){let t=e.closest(".clickable__5c90e");t&&!t.classList.contains("disabled__65fca")&&t.click()}})},50))}function tC(e){iv.c?(clearInterval(iv.c),iv.c=null,upd(e,"c",!1)):(upd(e,"c",!0),iv.c=setInterval(async()=>{if(isC||clk(["ไปต่อ","Continue","กลับ","Back"]))return;let e=document.querySelector(".sequences__34527");if(e){isC=!0;for(let t of e.querySelectorAll("img")){let l=t.getAttribute("alt");l&&(document.dispatchEvent(new KeyboardEvent("keydown",{key:l,code:l,bubbles:!0})),document.dispatchEvent(new KeyboardEvent("keyup",{key:l,code:l,bubbles:!0})),await new Promise(e=>setTimeout(e,40)))}return await new Promise(e=>setTimeout(e,500)),void(isC=!1)}document.querySelectorAll(".visibleText__65fca").forEach(e=>{if(["สร้าง","Craft"].includes(e.textContent)){let t=e.closest(".clickable__5c90e");t&&!t.classList.contains("disabled__65fca")&&t.click()}})},200))}function tCb(e){iv.cb?(clearInterval(iv.cb),iv.cb=null,upd(e,"cb",!1)):(upd(e,"cb",!0),iv.cb=setInterval(()=>{if(clk(["ไปต่อ","Continue","กลับ","Back"]))return;let e=document.querySelector('img[alt="target"]');if(e)return void(e.closest(".clickable__5c90e")||e).click();document.querySelectorAll(".visibleText__65fca").forEach(e=>{if(["การต่อสู้","Combat","Battle"].includes(e.textContent)){let t=e.closest(".clickable__5c90e");t&&!t.classList.contains("disabled__65fca")&&t.click()}})},100))}const p=document.createElement("div");p.id="lm-bot-panel";const h=document.createElement("div");h.className="lm-header";const tt=document.createElement("div");tt.className="lm-title",tt.innerText=txt[lng].t;const lb=document.createElement("button");lb.className="lm-lang-btn",lb.innerText="🇹🇭 TH";const bA=document.createElement("button"),bC=document.createElement("button"),bCb=document.createElement("button"),bX=document.createElement("button");function ref(){tt.innerText=txt[lng].t,lb.innerText="th"===lng?"🇹🇭 TH":"🇺🇸 EN",upd(bA,"a",!!iv.a),upd(bC,"c",!!iv.c),upd(bCb,"cb",!!iv.cb),bX.innerText=txt[lng].x}lb.onclick=()=>{lng="th"===lng?"en":"th",ref()},bA.onclick=()=>tA(bA),bC.onclick=()=>tC(bC),bCb.onclick=()=>tCb(bCb),bX.className="lm-btn btn-close",bX.onclick=()=>{clearInterval(iv.a),clearInterval(iv.c),clearInterval(iv.cb),p.remove(),st.remove(),console.log("Bot Stopped & Removed")},h.appendChild(tt),h.appendChild(lb),p.appendChild(h),p.appendChild(bA),p.appendChild(bC),p.appendChild(bCb),p.appendChild(bX),document.body.appendChild(p),ref();
```

---

## ⚠️ Disclaimer / ข้อควรระวัง
**[EN]** This project is for educational purposes only. Using automated scripts, bots, or macros on Discord may violate their Terms of Service. Use at your own risk. The developer is not responsible for any bans, penalties, or consequences that may occur to your account.

**[TH]** โปรเจกต์นี้จัดทำขึ้นเพื่อการศึกษาเท่านั้น การใช้สคริปต์อัตโนมัติ (Bot/Macro) บนแพลตฟอร์ม Discord อาจขัดต่อเงื่อนไขการให้บริการ (Terms of Service) ผู้ใช้งานควรใช้งานด้วยความระมัดระวัง ผู้พัฒนาจะไม่รับผิดชอบต่อผลกระทบใดๆ ที่เกิดขึ้นกับบัญชีผู้ใช้ของคุณ

---
*Created with ❤️ by [RoxyZ]*
