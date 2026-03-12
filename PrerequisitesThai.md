**สามารถติดตั้งและใช้งานบน Windows 11 ได้แน่นอนครับ!** 
เนื่องจาก A2UI เป็นโปรเจกต์ที่ทำงานอยู่บน **Node.js** (สำหรับฝั่งหน้าบ้าน/Client) และ **Python** (สำหรับฝั่งหลังบ้าน/Agent) ซึ่งเครื่องมือเหล่านี้รองรับการทำงานบน Windows อย่างสมบูรณ์ครับ

นี่คือขั้นตอนการติดตั้งและรันตัวอย่าง "Restaurant Finder" (แอปค้นหาร้านอาหาร) บน Windows 11 ครับ:

### 1. สิ่งที่ต้องติดตั้งไว้ในเครื่องก่อน (Prerequisites)
ก่อนเริ่ม โปรดตรวจสอบให้แน่ใจว่าเครื่อง Windows 11 ของคุณติดตั้งโปรแกรมเหล่านี้แล้ว:
* **[Git](https://git-scm.com/downloads)** (สำหรับ Clone โปรเจกต์)
* **[Node.js](https://nodejs.org/)** (มาพร้อมกับ `npm` สำหรับรันฝั่ง Client)
* **[Python](https://www.python.org/downloads/)** (สำหรับรันฝั่ง Agent)
* **[uv](https://github.com/astral-sh/uv)** (Python Package Manager ที่รันเร็วมาก สามารถติดตั้งผ่าน PowerShell ได้ด้วยคำสั่ง `pip install uv`)
* **Gemini API Key**: ไปสร้าง API Key ได้ฟรีที่ [Google AI Studio](https://aistudio.google.com/)

---

### 2. ขั้นตอนการติดตั้งและรันระบบ

เปิด **PowerShell** หรือ **Command Prompt** (Terminal) ของ Windows แล้วทำตามขั้นตอนต่อไปนี้ครับ:

**ขั้นตอนที่ 1: Clone โปรเจกต์ลงมาที่เครื่อง**
```powershell
git clone https://github.com/google/A2UI.git
cd A2UI
```

**ขั้นตอนที่ 2: ตั้งค่า API Key**
(แทนที่ `YOUR_API_KEY` ด้วยคีย์จริงที่คุณได้จาก AI Studio)
* **ถ้าใช้ PowerShell:**
  ```powershell
  $env:GEMINI_API_KEY="YOUR_API_KEY"
  ```
* **ถ้าใช้ Command Prompt (CMD):**
  ```cmd
  set GEMINI_API_KEY="YOUR_API_KEY"
  ```

**ขั้นตอนที่ 3: รันฝั่ง Backend (Agent)**
ใน Terminal เดิมที่ตั้งค่า API Key ไว้ ให้รันคำสั่งนี้เพื่อสตาร์ทเซิร์ฟเวอร์ฝั่ง AI:
```powershell
cd samples/agent/adk/restaurant_finder
uv run .
```

**ขั้นตอนที่ 4: รันฝั่ง Frontend (Client)**
ให้ **เปิดหน้าต่าง Terminal หรือ PowerShell ขึ้นมาใหม่** (อย่าปิดหน้าต่างเดิมที่รัน Agent ไว้) และรันคำสั่งเหล่านี้ทีละบรรทัดจากโฟลเดอร์ `A2UI` หลัก เพื่อทำการ Build ส่วนประกอบต่างๆ:

```powershell
# 1. ติดตั้งและ Build ตัว Web Core library
cd renderers/web_core
npm install
npm run build

# 2. ไป Build ตัว Markdown renderer
cd ../markdown/markdown-it
npm install
npm run build

# 3. ถอยกลับมาและไป Build ตัว Lit renderer
cd ../../lit
npm install
npm run build

# 4. ถอยกลับมาและไปรัน Shell Client (หน้าต่างแชท)
cd ../../samples/client/lit/shell
npm install
npm run dev
```

หลังจากคำสั่ง `npm run dev` ทำงานเสร็จ ตัวระบบจะแสดง URL (โดยปกติจะเป็น `http://localhost:5173` หรือคล้ายกัน) ให้คุณนำ URL นี้ไปเปิดในเบราว์เซอร์บน Windows 11 เพื่อทดลองใช้งานแชทบอทแบบมี UI (A2UI) ได้เลยครับ!