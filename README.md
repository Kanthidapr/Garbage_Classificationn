# Garbage Classification CNN — Render Single Service

โปรเจกต์นี้รวม Frontend + FastAPI Backend + CNN inference ไว้ใน Render Web Service เดียว

## โครงสร้าง
```text
garbage_classification_render_single/
├── app.py
├── requirements.txt
├── render.yaml
├── README.md
├── model/
│   ├── trash_class_cnn_mvp.keras
│   └── metadata.json
└── static/
    ├── index.html
    ├── script.js
    └── style.css
```

## สำคัญ
ไฟล์ `.keras` จริงไม่ได้อยู่ในไฟล์ ZIP นี้ เพราะเป็น model artifact ที่สร้างจากโปรเจกต์เดิม

ให้นำ:
`trash_class_cnn_mvp.keras`

มาใส่ที่:
`model/trash_class_cnn_mvp.keras`

## Deploy บน Render
1. Push โฟลเดอร์นี้ขึ้น GitHub
2. Render → New → Web Service
3. เลือก repository
4. Build Command:
```bash
pip install -r requirements.txt
```
5. Start Command:
```bash
uvicorn app:app --host 0.0.0.0 --port $PORT
```
6. Deploy

เว็บไซต์และ API จะอยู่ URL เดียวกัน เช่น:
`https://garbage-classification.onrender.com`

Frontend เรียก API แบบ relative path จึงไม่ต้องใส่ API URL และไม่ต้องสร้าง Render service ตัวที่สอง

## API
- `/` หน้าเว็บ
- `/health` ตรวจสถานะ
- `/info` ข้อมูลโมเดล
- `/predict` รับรูปและคืน Top 5 predictions
