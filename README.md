# 🚗 ANPR‑Parking‑Automation‑System

ANPR Parking Automation System is a **Node.js‑based smart parking solution** that integrates ANPR cameras, PLC‑controlled boom barriers, and a MySQL database.  
It automates vehicle entry / exit, enforces whitelist and slot limits, uploads number‑plate images, logs each event, and sends real‑time Telegram alerts with captured photos.

---

## 🧭 Features
- Automatic vehicle recognition using ANPR cameras  
- Whitelist / Blacklist verification  
- Company‑wise parking limit enforcement  
- Boom barrier control via PLC  
- Real‑time Telegram alerts with plate images  
- Live hourly and company‑wise count tracking  
- Dummy data insertion if a camera is idle for 1 hour  
- Auto‑recovery from internet or power outages  

---

## ⚙️ Tech Stack
- **Node.js + Express** – backend server  
- **MySQL** – data storage  
- **PLC Integration** – boom barrier control  
- **Telegram Bot API** – instant notifications  
- **ANPR Image API** – cloud image saving and retrieval  

---

## 🧩 Project Structure
app.js → main server and endpoints
database.js → database & cache handling
plc.js → PLC control methods
/anpr_images → uploaded number‑plate images

text


---

## 🚦 Endpoints
| Endpoint | Description |
|-----------|--------------|
| `/new-plate-parking-entry-1` | Handles vehicle parking entry detection |
| `/new-plate-parking-exit-1`  | Handles vehicle parking exit detection  |
| `/new-plate-main-entry-1` | Handles vehicle main entry detection |
| `/new-plate-main-exit-1`  | Handles vehicle main exit detection  |

---

## 💻 Setup Guide
```bash
# Clone repository
git clone https://github.com/<your_username>/ANPR-Parking-Automation-System.git
cd ANPR-Parking-Automation-System

# Install dependencies
npm install

# Configure your database credentials in database.js

# Start the server
node app.js
Server runs on port 2202

🕹️ Example Payload
JSON

{
  "plate": "MH03DG8756",
  "plateimage": "<base64 encoded image>"
}
📊 Database Tables
Table	Purpose
lightbridge_numberplate_whitelist	Authorized vehicle list
lightbridge_company_parking_limits	Slot limits per company
lightbridge_vehicle_count_hourly	Hourly in/out counts
lightbridge_company_live_count	Real‑time live counts
lightbridge_anpr_logs	Raw entry/exit records
lightbridge_bad_numbers	Blocked plates database

🧠 System Logic Summary
Load whitelist, company limits, and live counts at startup.
For each camera endpoint, if idle ≥ 1 hour → insert dummy log.
On vehicle entry:
Verify in whitelist.
Upload image → update counts → open boom or send Telegram alert with photo.
On vehicle exit:
Update counts, log event, always open boom.
Store live counts to DB every minute.
On restart, reload live state from DB for continuity.

📢 Alerts
Un‑whitelisted vehicle → Telegram alert + number‑plate photo.
Parking limit exceeded → Telegram alert + photo.

📜 License
© 2024 Claypot Technologies · All Rights Reserved

