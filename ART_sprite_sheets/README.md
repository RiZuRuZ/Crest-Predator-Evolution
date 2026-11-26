# ART — Sprite sheets ของ Crest Predator Evolution (v27)

ภาพทั้งหมดในโฟลเดอร์ `sprite_sheets/` ดึงออกมาจาก `GameSRC/CrestPredatorV27.html` (ชุดภาพที่เกมเวอร์ชันคอมใช้ ซึ่งมาจากชุดเดียวกับ ROM บนบอร์ด สี 12 บิต)

> **ไม่ใช่ไฟล์ต้นฉบับของผู้ออกแบบ** — เป็นภาพที่ export แล้ว ใช้ดู อ้างอิง และนำไปใช้ในรายงานหรือสไลด์ได้ ถ้าต้องการแก้ sprite หรือสร้าง `.mem` ใหม่ ต้องใช้ไฟล์ต้นฉบับ (เฟรม PNG ที่ `tools/build_prop_roms.py` และ `tools/build_boss.py` อ่าน) ซึ่งไม่ได้อยู่ใน repo ตอนนี้

ทุกไฟล์เรียงเฟรมแนวนอนในภาพเดียว (เฟรมกว้างเท่ากัน) ดูภาพรวมได้ที่ `overview_x2.png` และรายละเอียดขนาดใน `manifest.json`

| ไฟล์ | ขนาดต่อเฟรม (px) | จำนวนเฟรม | รูปแบบ |
|---|---|---|---|
| `bg.png` | 960×320 | 1 | single image |
| `dragon1.png` | 73×41 | 10 | frames side by side |
| `dragon2.png` | 96×58 | 10 | frames side by side |
| `dragon3.png` | 126×74 | 10 | frames side by side |
| `dragon4.png` | 171×106 | 10 | frames side by side |
| `fish0.png` | 31×27 | 4 | frames side by side |
| `fish1.png` | 52×42 | 4 | frames side by side |
| `fish2.png` | 93×52 | 4 | frames side by side |
| `fish3.png` | 44×35 | 4 | frames side by side |
| `redshark.png` | 93×52 | 4 | frames side by side |
| `boss_n.png` | 118×57 | 6 | frames side by side |
| `boss_red.png` | 118×57 | 6 | frames side by side |
| `boss_p2.png` | 118×57 | 6 | frames side by side |
| `boss_p3.png` | 118×57 | 6 | frames side by side |
| `boss_flash.png` | 118×57 | 6 | frames side by side |
| `mine.png` | 43×44 | 4 | frames side by side |
| `boom.png` | 64×64 | 6 | frames side by side |
| `jelly.png` | 37×52 | 4 | frames side by side |
| `harp_h.png` | 88×23 | 4 | frames side by side |
| `harp_v.png` | 23×88 | 4 | frames side by side |
| `powerup.png` | 24×24 | 3 | frames side by side |
| `seaweed.png` | 61×93 | 8 | frames side by side |
| `shadow.png` | 118×57 | 1 | single image |

หมายเหตุ: `bg.png` คือพื้นหลังครึ่งความละเอียด 960×320 ที่เกมขยาย 2×2 เป็น 1920×640
