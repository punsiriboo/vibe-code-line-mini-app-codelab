# Punsiri's Codelabs

Code lab สำหรับการสร้าง LINE MINI App ด้วย Vibe Coding ใน Google AI Studio

## Codelab

📁 `vibe-coding-line-mini-app-in-ai-studio/`

**Vibe Coding LINE MINI App with AI Studio** — สอนการสร้างเว็บจองร้านอาหาร แปลงเป็น LINE MINI App และส่ง Service Message ทั้งหมดด้วย Prompt ใน Google AI Studio

## สิ่งที่ต้องเตรียม

ก่อนที่จะ build codelab คุณต้องมีสิ่งต่อไปนี้:

Ref: https://github.com/googlecodelabs/tools/tree/main/claat

- **Go** (Go Programming Language) — สำหรับติดตั้ง claat
  - macOS: `brew install go`
  - Linux: `sudo apt-get install golang-go`
  - หรือดาวน์โหลดจาก: https://golang.org/dl/

สำหรับ deploy ขึ้น Google Cloud Storage (ถ้าต้องการ):

- **Google Cloud SDK** (`gcloud`, `gsutil`) — https://cloud.google.com/sdk/docs/install
- บัญชี GCP ที่มีสิทธิ์เขียนไปยัง bucket ปลายทาง

## วิธี Build Codelab

### วิธีที่ 1: ใช้ build.sh (แนะนำ)

```bash
cd vibe-coding-line-mini-app-in-ai-studio
./build.sh
```

สคริปต์ `build.sh` จะทำสิ่งต่อไปนี้:

1. ✅ ตรวจสอบว่ามี `claat` ติดตั้งหรือยัง
2. ✅ ถ้ายังไม่มี จะติดตั้ง `claat` อัตโนมัติ
3. ✅ Export markdown file (`vibe-coding-line-mini-app.md`) เป็น HTML
4. ✅ สร้างโฟลเดอร์ `codelab/` ที่มีไฟล์ HTML พร้อมใช้งาน

### วิธีที่ 2: ระบุไฟล์และโฟลเดอร์ output เอง

```bash
cd vibe-coding-line-mini-app-in-ai-studio
./build.sh vibe-coding-line-mini-app.md codelab
```

## วิธี Deploy Codelab

```bash
cd vibe-coding-line-mini-app-in-ai-studio
./deploy.sh --build
```

สคริปต์ `deploy.sh` จะอัปโหลดโฟลเดอร์ `codelab/` ไปยัง Google Cloud Storage

- ใช้ `--build` เพื่อ build ก่อน deploy
- ถ้า build แล้ว รัน `./deploy.sh` ได้เลย

URL หลัง deploy:

https://storage.googleapis.com/codelabs-beat-beat/vibe-coding-line-mini-app-in-ai-studio/index.html

## โครงสร้างโปรเจค

```
vibe-code-line-mini-app-codelab/
├── vibe-coding-line-mini-app-in-ai-studio/
│   ├── build.sh                          # สคริปต์สำหรับ build codelab
│   ├── deploy.sh                         # สคริปต์สำหรับ deploy ขึ้น GCS
│   ├── vibe-coding-line-mini-app.md      # ไฟล์ markdown หลัก
│   ├── img/                              # รูปภาพที่ใช้ใน codelab
│   └── codelab/                          # โฟลเดอร์ผลลัพธ์หลังจาก build (HTML)
│       ├── index.html                    # ไฟล์ HTML หลัก
│       ├── codelab.json                  # ไฟล์ metadata
│       └── img/                          # รูปภาพที่ถูก copy มา
└── README.md
```

## Troubleshooting

### ปัญหา: claat command not found

**แก้ไข:**

- ตรวจสอบว่า Go ติดตั้งแล้ว: `go version`
- ติดตั้ง claat: `go install github.com/googlecodelabs/tools/claat@latest`
- เพิ่ม `$HOME/go/bin` ใน PATH: `export PATH="$PATH:$HOME/go/bin"`

### ปัญหา: Permission denied เมื่อรัน build.sh หรือ deploy.sh

**แก้ไข:**

```bash
chmod +x build.sh deploy.sh
```

### ปัญหา: Build ล้มเหลว

**แก้ไข:**

- ตรวจสอบว่าไฟล์ markdown มีอยู่ (`vibe-coding-line-mini-app.md`)
- ตรวจสอบว่ามีรูปภาพในโฟลเดอร์ `img/` ครบถ้วน
- ตรวจสอบ error message จาก claat
- ตรวจสอบว่า path ของรูปภาพใน markdown ถูกต้อง (เช่น `img/xxx.png`)

### ปัญหา: Deploy ล้มเหลว

**แก้ไข:**

- ตรวจสอบว่า `gcloud` และ `gsutil` ติดตั้งแล้ว
- ล็อกอิน GCP: `gcloud auth login`
- ตรวจสอบว่ามี `codelab/index.html` แล้ว (รัน `./build.sh` ก่อน)

## หมายเหตุ

- โฟลเดอร์ `codelab/` จะถูกสร้างใหม่ทุกครั้งที่ build
- ไฟล์ใน `codelab/` จะถูกเขียนทับทุกครั้งที่ build ใหม่
- ควร commit และ push เฉพาะไฟล์ markdown (`.md`) และ `img/` เท่านั้น ไม่จำเป็นต้อง commit `codelab/`

## ลิงก์ที่เกี่ยวข้อง

- [Google Codelabs Tools (claat)](https://github.com/googlecodelabs/tools)
- [Format Guide](https://github.com/googlecodelabs/tools/blob/main/FORMAT-GUIDE.md)
- [Google AI Studio](https://aistudio.google.com/)
- [LINE Developers Console](https://developers.line.biz/console/)
