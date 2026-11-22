# Crest Predator Evolution

เกมมังกรทะเลวิวัฒนาการ เขียนด้วย **Verilog** บนบอร์ด **Digilent Nexys A7-100T** (Artix-7 XC7A100T) แสดงผลผ่าน VGA — โปรเจกต์รายวิชาของทีม (เวอร์ชันล่าสุด **v27**)

ผู้เล่นเป็น "มังกรทะเล" ตัวเล็ก ว่ายในโลกใต้ทะเล กินปลาที่เล็กกว่าเพื่อเก็บ Evolution Point (EP) วิวัฒนาการผ่าน 4 ร่าง หลบอันตราย (ทุ่นระเบิด แมงกะพรุน ฉมวก ฉลามแดง ฉลามยักษ์) จัดการ Oxygen และหัวใจ เล่นมินิเกม event ทุก 50 วินาที เมื่อ EP ถึง 500 จะเข้าสู่การต่อสู้กับบอส — ชนะบอส = WIN พร้อมเกรด

## ไฟล์ใน repository

| ไฟล์ | คืออะไร |
|---|---|
| [`cpe v27 full.zip`](cpe%20v27%20full.zip) | source code ทั้งหมดของ v27: `src/` (76 ไฟล์ .v = 78 module, 51 ไฟล์ .mem), `constraints/nexys_a7.xdc`, `sim/` (testbench 24 ไฟล์), `tools/` (script สร้าง ROM / เพลง), `CHANGES_v27.txt` |
| [`CrestPredator_AllDetails_v4 D.pdf`](CrestPredator_AllDetails_v4%20D.pdf) | เอกสารรายละเอียดทั้งหมด (198 หน้า): ภาค 1 ภาพรวมเกม (หัวข้อ 1–20), ภาค 2 ข้อมูลเชิงลึก — การ์ดโมดูล, ค่าคงที่, ภาพ .mem, ผังสัญญาณ top.v, testbench, ตาราง transition FSM, pipeline, เพลง, ทรัพยากร FPGA, draw.io รายหน้า (หัวข้อ 21–31) |
| [`crest_predator_state_diagrams_v27.drawio`](crest_predator_state_diagrams_v27.drawio) | state diagram ทั้งหมด 36 หน้า (00 Index + 01–35) เปิดด้วย [draw.io / diagrams.net](https://app.diagrams.net) |
| [`Notion workplan cpe.csv`](Notion%20workplan%20cpe.csv) | ตารางแผนงานจาก Notion (104 งาน, หมวด / สถานะ / รายละเอียด) |
| [`CrestPredatorV27.html`](CrestPredatorV27.html) | เกมเวอร์ชันคอม v27 — ไฟล์เดียว เปิดในเบราว์เซอร์แล้วเล่นได้ทันที มีแผงจำลองบอร์ด (สวิตช์ LED 7-segment ปุ่ม) ใต้จอเกม (ดูหัวข้อ "เล่นบนคอม") |

## เล่นบนคอม

ดาวน์โหลด `CrestPredatorV27.html` แล้วดับเบิลคลิกเปิดด้วยเบราว์เซอร์ (Chrome / Edge / Firefox) — ไม่ต้องติดตั้งอะไร ไฟล์รวมภาพ เสียง และเพลงไว้ในตัว (เพลงใช้โมเดลเดียวกับบอร์ด) เสียงเริ่มเล่นหลังกดปุ่มหรือคลิกครั้งแรก

> GitHub จะแสดงไฟล์ .html เป็นโค้ด ไม่ได้รันให้ ต้องดาวน์โหลดไปเปิดเอง

| คีย์บอร์ด | เท่ากับบนบอร์ด |
|---|---|
| ลูกศร หรือ W A S D | BTNU / BTND / BTNL / BTNR |
| Space หรือ Enter | BTNC |
| P | SW0 Pause |
| M | SW1 Mute |
| 1 2 3 4 5 6 7 8 9 0 - = | SW2–SW13 (สับสวิตช์) |
| T | SW14 เอียงบอร์ด (คอมไม่มีเซนเซอร์) |
| V | SW15 ไมโครโฟน — กด **R** ค้างแทนการตะโกน |

คลิกเมาส์ที่สวิตช์และปุ่มบนแผงจำลองบอร์ดได้ด้วย · ตอนโดนบอสงับ ให้กดปุ่มรัวแทนการเขย่าบอร์ด

## ฮาร์ดแวร์และผล build (v27)

| หัวข้อ | ค่า |
|---|---|
| บอร์ด | Nexys A7-100T (XC7A100T-1CSG324C) |
| จอภาพ | VGA 640×480 @ 60 Hz, สี 12 บิต |
| Clock | 100 MHz → MMCM → 25 MHz (1 clock = 1 pixel), clock domain เดียว, game tick 60 Hz |
| Timing | WNS +7.567 ns |
| ทรัพยากร | LUT 49,018 · FF 7,274 · BRAM 132 / 135 (RAMB36 131 + RAMB18 2) · DSP 103 |
| เครื่องมือ | Vivado 2024.2 |
| I/O ที่ใช้ | VGA, ปุ่ม 5 + CPU_RESET, สวิตช์ 16, LED 16, RGB LED 2, 7-segment 8 หลัก, Audio PWM (mono), ไมโครโฟน PDM, Accelerometer ADXL362 (SPI), คีย์บอร์ด USB (PS/2 ผ่าน PIC24) |

## วิธี build

1. แตกไฟล์ `cpe v27 full.zip`
2. Vivado → New Project → RTL Project → part **xc7a100tcsg324-1**
3. Add Sources: ไฟล์ทั้งหมดใน `src/` (ทั้ง `.v` และ `.mem` — รวม 127 ไฟล์) และตั้ง `top.v` เป็น top module
4. Add Constraints: `constraints/nexys_a7.xdc`
5. (ถ้าต้องการ) Add Simulation Sources: ไฟล์ใน `sim/`
6. Run Synthesis → Implementation → Generate Bitstream → Program Device

> ไฟล์ `.mem` ต้องอยู่ใน project เดียวกัน (`$readmemh`) ไม่อย่างนั้น ROM ภาพ / เพลงจะว่าง

## การควบคุม

| อินพุต | หน้าที่ |
|---|---|
| BTNU / BTND / BTNL / BTNR | ว่าย 4 ทิศ (ทแยงได้) · ที่ TITLE ซ้าย/ขวา = เลือก EASY / NORMAL / HARD · ใช้ในมินิเกม |
| BTNC | เริ่มเกม · Dash · ตอน PAUSE = เปิด/ปิดเพลง |
| CPU_RESET | reset ทั้งระบบ |
| SW0 | Pause |
| SW1 | Mute เสียงทั้งหมด |
| SW2–SW13 | มินิเกมสับสวิตช์ (LED เหนือสวิตช์กะพริบ = ต้องสับ) |
| SW14 | บังคับด้วยการเอียงบอร์ด |
| SW15 | เปิดไมโครโฟน (ตะโกน = Tidal Roar / PERFECT ROAR) |
| คีย์บอร์ด USB | W A S D + Space (ยังทดสอบไม่ผ่านกับคีย์บอร์ดที่มี) |

รายละเอียดเต็มอยู่ในเอกสาร AllDetails หัวข้อ 4

## ภาพรวมเกม

- **4 ร่าง:** EP 25 → ร่าง 2, 75 → ร่าง 3, 200 → ร่าง 4, 500 → บอส
- **อันตราย:** ฉมวก, ทุ่นระเบิด, แมงกะพรุน, ฉลามแดง (ร่าง 2+), ฉลามยักษ์ (ซ่อนในสาหร่าย + มินิเกมสับสวิตช์)
- **Event ทุก 50 วินาที:** หลบหอก → กดลูกศร → แถบจังหวะ (วนซ้ำ)
- **บอส:** HP 12, 3 เฟส, 18 state — พุ่งชน, ฟอง, งับ, ทุ่น, สับสวิตช์, หลบหอก, ปิดท้ายด้วยมินิเกมลูกศร
- **เพลง:** 5 track แบบ 16-bit (wavetable 4 เสียง + กลอง 1 เสียง) 48,828 Hz
- **ความยาก:** EASY / NORMAL / HARD

## โครงสร้าง source (ใน zip)

```
src/            76 ไฟล์ .v (78 module) + 51 ไฟล์ .mem   top.v = top module
constraints/    nexys_a7.xdc
sim/            testbench 24 ไฟล์ (tb_*.v)
tools/          Python script สร้าง ROM ภาพ, ฟอนต์, แมพ, บอส, เพลง (tools/music16)
CHANGES_v27.txt สิ่งที่เปลี่ยนใน v27
```

## ข้อควรรู้

- ค่าเวลา / ความเร็ว / ขนาดในโค้ดส่วนใหญ่มีป้าย `PLACEHOLDER` คือค่าที่ทีมจูนจากการเล่น
- คอมเมนต์บางจุดในโค้ดเป็นของเวอร์ชันเก่า (เช่น "pixel changes every 4 clocks") — พฤติกรรมจริงดูจากโค้ดและเอกสาร AllDetails หัวข้อ 20
- draw.io v27 หน้า 23 ยังไม่มีเส้น "ชนทุ่นตอนบอสเหลือ HP 1 → ARROW" และหน้า 35 dev_cheat เป็นแบบย่อ (โค้ดถูกต้อง)

## ทีมผู้พัฒนา

| สมาชิก | รหัสนักศึกษา | บทบาท | ความรับผิดชอบ |
|---|---|---|---|
| ภูริ เตชตรีสุคนธ์ | | Lead Developer / Hardware & Game Engineer | ออกแบบ game mechanics และสถาปัตยกรรมระบบ · พัฒนา Verilog ทั้งหมด 78 module พร้อม constraints (XDC) และ testbench · แปลงกราฟิกเป็น ROM (.mem) และพัฒนาเครื่องมือใน `tools/` · ออกแบบเพลงและเสียงประกอบ · synthesize และทดสอบบนบอร์ด Nexys A7-100T · พัฒนาเกมเวอร์ชันคอม (`CrestPredatorV27.html`) · วางแผนงานใน Notion · จัดทำเอกสาร AllDetails และ README |
| นิพาดา สันธนาคร | 68070501025 |  Visual & Presentation Designer | ออกแบบ sprite และ animation ของตัวละคร · จัดทำ state diagram · จัดทำสไลด์นำเสนอ |
| ทิวัตถ์ แพงสาร | 68070501069 | Visual & Presentation Designer | ออกแบบ sprite และ animation ของตัวละคร · จัดทำ state diagram · จัดทำสไลด์นำเสนอ |
| พรหมพิริยะ พงษ์สกุล | 68070501076 | Visual & Presentation Designer | ออกแบบ sprite และ animation ของตัวละคร · จัดทำ state diagram · จัดทำสไลด์นำเสนอ |
| ศักรนันท์ ศรีสวัสดิ์ | 68070501085 | Technical Writer | เรียบเรียงและจัดทำรายงานโครงงาน |



## รายวิชา

<!-- TODO: ใส่รหัสวิชา / ชื่อวิชา / อาจารย์ / มหาวิทยาลัย -->
_(ใส่ข้อมูลรายวิชา)_
