# Frontend

Frontend ของ Ani-Web พัฒนาด้วย Next.js และ React โดยหน้าเว็บเรียก Backend API และ file server ที่รันแยกกัน

## เริ่มใช้งาน

จาก root ของ repository:

```bash
cd frontend
npm ci
npm run dev
```

เปิด [http://localhost:3000](http://localhost:3000) โดยต้องเริ่ม backend API และ file server ก่อนหรือใน terminal แยกกันด้วย ดูคำสั่งครบทุก service, การตั้งค่า และข้อจำกัดได้ที่ [README หลัก](../README.md)

## Scripts

| คำสั่ง | รายละเอียด |
| --- | --- |
| `npm run dev` | เริ่ม development server |
| `npm run build` | สร้าง production build |
| `npm start` | เริ่ม server จาก production build |
