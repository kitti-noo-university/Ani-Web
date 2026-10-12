# Ani-Web

Ani-Web เป็น mini-project สำหรับแสดงและจัดการข้อมูลอนิเมะรายสัปดาห์ พร้อมหน้าเข้าสู่ระบบและสมัครสมาชิก โปรเจกต์นี้ใช้เพื่อการศึกษาและทดลองใช้งาน ไม่ควรนำระบบ authentication หรือ configuration ปัจจุบันไปใช้กับ production

## ฟีเจอร์

- แสดงรายการอนิเมะและกรองตามวันในสัปดาห์
- เพิ่ม แก้ไข และลบข้อมูลอนิเมะ
- สมัครสมาชิก เข้าสู่ระบบ ออกจากระบบ และตรวจสอบ profile ด้วย JWT
- แสดงภาพประกอบและมี API สำหรับอัปโหลด/ดาวน์โหลดไฟล์

ข้อมูลอนิเมะและผู้ใช้ตัวอย่างเก็บไว้ในหน่วยความจำใน `backend/database.js` จึงจะกลับไปเป็นข้อมูลเริ่มต้นเมื่อ restart API ไม่มีฐานข้อมูลหรือบริการภายนอกที่ต้องตั้งค่า

## เทคโนโลยี

- Frontend: Next.js, React, Axios และ SWR
- Backend API: Node.js, Express และ Passport (Local/JWT)
- File server: Express และ Multer

## โครงสร้างโปรเจกต์

```text
.
├── backend/
│   ├── index.js                 # API สำหรับอนิเมะและ authentication
│   ├── server.js                # file server และ upload API
│   ├── database.js              # ข้อมูลตัวอย่างในหน่วยความจำ
│   └── src/                     # routes, controller และ upload middleware
└── frontend/
    ├── pages/                   # หน้า Next.js
    ├── components/              # layout, navigation และ auth wrappers
    └── config/config.js         # URL ของ API ตาม NODE_ENV
```

## สิ่งที่ต้องมี

- Node.js และ npm
- Git
- พอร์ต `80`, `3000` และ `8080` ว่างสำหรับ API, frontend และ file server ตามลำดับ

ไม่มีไฟล์ `.env` ที่ต้องสร้างเพื่อเริ่มต้นใช้งาน โดย frontend เลือก API URL จาก `NODE_ENV` ใน `frontend/config/config.js`; ค่าเริ่มต้นสำหรับ development คือ `http://localhost/api` ส่วน backend API ใช้ `PORT` หากกำหนด และใช้พอร์ต `80` เมื่อไม่ได้กำหนด `backend/server.js` ใช้พอร์ต `8080` โดยตรง

## ติดตั้งและเริ่มทำงาน

Clone repository และเข้าโฟลเดอร์โปรเจกต์:

```bash
git clone <repository-url>
cd Ani-Web
```

เปิด terminal แยกกัน 3 หน้าต่าง และสั่งจาก root ของ repository:

**Terminal 1 — Backend API** (รับคำขอที่ `http://localhost:80/api`)

```bash
cd backend
npm install
node index.js
```

**Terminal 2 — File server** (ให้บริการไฟล์ที่ `http://localhost:8080`)

```bash
cd backend
node server.js
```

**Terminal 3 — Frontend** (เปิดเว็บที่ `http://localhost:3000`)

```bash
cd frontend
npm ci
npm run dev
```

เปิด `http://localhost:3000` ใน browser โดยต้องเปิด backend API และ file server ค้างไว้ด้วย

> Backend API กำหนดพอร์ตเริ่มต้นเป็น `80` ซึ่งบางระบบปฏิบัติการอาจต้องใช้สิทธิ์พิเศษเพื่อ bind พอร์ตนี้ หากเปลี่ยน `PORT` ต้องปรับ URL ใน `frontend/config/config.js` ให้ตรงกับพอร์ต API ด้วย ส่วน file server ยังใช้พอร์ต `8080`

## Scripts

| ส่วน | คำสั่ง | รายละเอียด |
| --- | --- | --- |
| Frontend | `npm run dev` | เริ่ม Next.js development server |
| Frontend | `npm run build` | สร้าง production build |
| Frontend | `npm start` | เริ่ม Next.js server จาก build ที่สร้างไว้ |
| Backend API | `node index.js` | เริ่ม API server |
| File server | `node server.js` | เริ่ม upload/download server |

Backend ไม่มี npm scripts สำหรับ start หรือ test; ใช้คำสั่ง `node` ตามตาราง

## API ที่มีใน source

Backend API ทุกเส้นทางด้านล่างมี prefix `/api`:

| Method | Path | การทำงาน |
| --- | --- | --- |
| `GET`, `POST` | `/api/animes` | ดูรายการและเพิ่มอนิเมะ |
| `GET`, `PUT`, `DELETE` | `/api/animes/:anime_id` | ดู แก้ไข หรือลบอนิเมะตาม ID |
| `POST` | `/api/register` | สมัครสมาชิก |
| `POST` | `/api/login` | เข้าสู่ระบบและรับ JWT |
| `GET` | `/api/profile` | ดู profile โดยส่ง ****** |
| `GET` | `/api/logout` | ล้าง authentication cookie |

File server แยกจาก API: `POST /upload`, `GET /files` และ `GET /files/:name` ที่พอร์ต `8080`

## การแก้ปัญหาเบื้องต้น

- **พอร์ตถูกใช้งานหรือเปิด server ไม่ได้:** ตรวจสอบพอร์ต `80`, `3000` และ `8080`; หากเปลี่ยนพอร์ต API ให้ปรับ URL ใน `frontend/config/config.js` ตามด้วย
- **เว็บแสดงข้อมูลไม่ได้:** ตรวจสอบว่า backend API ทำงานที่ URL ซึ่งกำหนดใน `frontend/config/config.js` และ frontend ทำงานที่ `http://localhost:3000`
- **อัปโหลดไฟล์ถูก browser ปฏิเสธด้วย CORS:** `backend/server.js` อนุญาต origin `http://localhost:8081` แต่ Next.js dev server ใช้ `http://localhost:3000`; ค่าเหล่านี้ไม่ตรงกันใน source ปัจจุบัน
- **ข้อมูลที่เพิ่มหายหลัง restart API:** เป็นพฤติกรรมปัจจุบัน เนื่องจากข้อมูลจัดเก็บในหน่วยความจำ ไม่ได้บันทึกลงฐานข้อมูล

ดูคำแนะนำแยกส่วนได้ที่ [Backend README](backend/README.md) และ [Frontend README](frontend/README.md)
