# Panduan Hosting MKC CBT (Vercel Serverless & Node.js)

## 1. Deploy ke Vercel (`vercel.json` + `api/index.js`)
Proyek ini sudah dilengkapi `vercel.json` dan serverless handler `api/index.js` (memuat bundel CommonJS `api/_server.cjs` yang dibangun otomatis oleh `npm run build`) sehingga route frontend (`dist/`) dan API backend (`/api/*`) berjalan dalam satu deployment Vercel.

Atur **Environment Variables** berikut di **Vercel Project Settings → Environment Variables**:
- `SESSION_SECRET`: string acak minimal 32 karakter (wajib sama antar serverless instance agar token login siswa/guru/super admin tetap valid).
- **Pilih salah satu database permanen** agar akun siswa, guru, bank soal, ujian, dan nilai tersimpan permanen antar serverless instance:
  1. **PostgreSQL (`DATABASE_URL` atau `POSTGRES_URL` — Paling Mudah / Gratis)**: Hubungkan **Neon** atau **Supabase** langsung dari tab **Storage** di dashboard Vercel (otomatis mengisi `DATABASE_URL` / `POSTGRES_URL`).
  2. **Firebase Admin (`FIREBASE_SERVICE_ACCOUNT_JSON`)**: Isi JSON (atau base64) **Firebase Service Account Key** bila memakai proyek Firebase standar dengan IAM aktif.

> **Penting**: Tanpa `DATABASE_URL`/`POSTGRES_URL` atau `FIREBASE_SERVICE_ACCOUNT_JSON`, Vercel tidak memiliki penyimpanan permanen antar-instance sehingga penambahan/impor siswa tidak akan tersimpan permanen.

## 2. Menjalankan Secara Lokal / VPS Node.js
```bash
npm install
npm run build
npm start
```

## 3. Catatan Keamanan Exam Mode
Browser web standar tidak dapat menjamin penguncian perangkat 100% pada tingkat sistem operasi. Untuk ujian berisiko tinggi, gunakan perangkat terkelola (*managed device* / Chromebook Kiosk) atau peramban ujian khusus (*Safe Exam Browser*).
