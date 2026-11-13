# API Test Console — ระบบแจ้งซ่อมคอมพิวเตอร์และอุปกรณ์ของวิทยาลัย

หน้าเว็บทดสอบ Back-End API ของโปรเจกต์
[`college-repair-api`](https://github.com/69319010015/college-repair-api) — ทดสอบยิงจริงทุก endpoint
(health, login, แจ้งซ่อม, เปลี่ยนสถานะตาม state machine, ดูรายการ) ผ่านเบราว์เซอร์ ไม่ต้องติดตั้งอะไร

## ใช้งาน

1. เปิดหน้า **[API Test Console](https://69319010015.github.io/repair-api-tester/)**
2. ใส่ **API Base URL** ที่ช่องบนสุด (ระบบจำค่าไว้ใน `localStorage` ของเบราว์เซอร์)
   - ค่าเริ่มต้น `http://localhost:3000` — ไม่ต้องใส่ `/api/v1` ก็ได้ ตัวหน้าเว็บเติมให้เอง
   - ถ้า API อยู่เครื่องอื่น เช่น `https://api.example.com` หรือ `http://192.168.1.50:8080`
3. กด **ทดสอบเชื่อมต่อ** (ยิง `GET /api/v1/health`)
4. กด **เข้าสู่ระบบทั้ง 2 คน** → **แจ้งซ่อม** → กดปุ่มสถานะทีละขั้น
   (`ACCEPTED → IN_PROGRESS → WAITING_PARTS → COMPLETED`) แล้วดู HTTP status + JSON ใน log ด้านขวา

## รัน Back-End ในเครื่องก่อน

```bash
git clone https://github.com/69319010015/college-repair-api.git
cd college-repair-api
npm install
npm start          # http://localhost:3000
```

ถ้า Back-End รันอยู่บนเซิร์ฟเวอร์อื่น ให้ทำ SSH tunnel มาที่เครื่องตัวเอง :

```bash
ssh -N -L 3000:172.17.0.3:3000 root@<vps-ip>
```

## หมายเหตุ

- หน้าถูกโฮสต์บน GitHub Pages (https) แต่ API ในเครื่องเป็น http — Chrome/Firefox ยอมให้เรียก
  `http://localhost` จากหน้า https ได้ แต่ถ้าเบราว์เซอร์บล็อก ให้ดาวน์โหลด `index.html`
  ไปเปิดในเครื่อง (file://) แทน
- API เปิด CORS แบบ `*` (สำหรับพัฒนา) จึงเรียกข้ามโดเมนได้จากหน้า Pages
- ไม่มีข้อมูลลับในไฟล์นี้ — token ออกใหม่จาก `/auth/login` ทุกครั้งที่กดใช้งาน
