# Backend

Backend ของ Ani-Web มี 2 services: API สำหรับอนิเมะและ authentication (`index.js`) และ file server สำหรับอัปโหลด/ดาวน์โหลด (`server.js`) ทั้งคู่ใช้ dependencies ใน `backend/package.json`

## เริ่มใช้งาน

จาก root ของ repository:

```bash
cd backend
npm install
node index.js
```

API ใช้พอร์ต `80` โดยค่าเริ่มต้น หรือ `PORT` หากกำหนดไว้ การเริ่ม file server ต้องใช้ terminal อีกหน้าต่างหนึ่ง:

```bash
cd backend
node server.js
```

File server ใช้พอร์ต `8080` ดูขั้นตอนตั้งค่าทั้งโปรเจกต์, endpoints และข้อจำกัดได้ที่ [README หลัก](../README.md)
