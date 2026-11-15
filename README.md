# Wyckoff Cycle Pro — Pine Script v6

ชุดอินดิเคเตอร์ Wyckoff สำหรับ TradingView (Pine Script v6) เน้นการอ่านวัฏจักรตลาดแบบ Wyckoff และช่วยวางแผน TP/SL จากโครงสร้างราคา

> **Disclaimer:** โค้ดเหล่านี้เป็นเครื่องมือช่วยวิเคราะห์ ไม่ใช่กลยุทธ์เทรดอัตโนมัติ และไม่สามารถส่งคำสั่งซื้อขายจริงได้

## ไฟล์ในโปรเจกต์

| ไฟล์ | รายละเอียด |
|---|---|
| `wyckoff_cycle_pro_v3.pine` | เวอร์ชันล่าสุด — ครบทุก event, 2 trade box (Breakout / Aggressive), TP-RANGE / TP-ENTRY, SL ตาม structure + ATR, dashboard |
| `wyckoff_cycle_pro_v2.pine` | เวอร์ชันก่อนหน้า — core cycle + trade box เดียว |
| `wyckoff_cycle_pro.pine` | เวอร์ชันแรก |
| `volume_wyckoff_v6.pine` | สคริปต์อ้างอิง volume/Wyckoff รุ่นก่อน |

## v3 Features

- ตรวจจับ Accumulation, Distribution, Markup, Markdown, Re-accumulation, Redistribution
- แสดง Phase A–E เป็นเส้นแนวตั้งแบบ dashed พร้อม label
- แสดง Wyckoff events:
  - Tier 1: SC/BC, AR, ST, Spring/UT, SOS/SOW, LPS/LPSY
  - Tier 2: PS, PSY, Shakeout, Test, No Supply, No Demand, UTAD, JAC, BUEC
  - Tier 3: Absorption, Effort vs Result, Exhaustion
- คะแนนรวม `SCORE 0–10` จากน้ำหนัก Tier 1 = 1.0, Tier 2 = 0.5, Tier 3 = 0.25
- Signal ต้องมี trigger + core event ขั้นต่ำ + คะแนนขั้นต่ำ
- TP ใช้ range projection:
  - `TP-RANGE` = projection จากขอบ range
  - `TP-ENTRY` = projection จาก entry
- SL = structure ± 1.5×ATR และ cap ที่ 4×ATR
- Trade box 2 ชุดต่อรอบ: `BOX B` (Breakout) และ `BOX A` (Aggressive)
- คำแนะนำ: `MARKET NOW`, `WAIT BREAKOUT`, `WAIT RETEST`, `NO TRADE`
- ธีมขาว/ดำ/เทา, LONG/SHORT, BIAS แยก Bullish/Bearish

## วิธีติดตั้ง

1. เปิด TradingView → Pine Editor
2. วางโค้ดจากไฟล์ `.pine`
3. กด Save → Add to chart
4. ตั้ง Alert เป็น **Once Per Bar Close**

## ค่าเริ่มต้นที่แนะนำ

- Minimum Score: `5.0`
- Minimum Core Events: `3`
- Structure SL Buffer: `1.5 ATR`
- Max SL Distance: `4.0 ATR`
- Max Trades Per Cycle Per Box: `1`

ถ้าต้องการให้ `BOX A` ออกเร็วขึ้นที่ Spring/ST ให้ลองลด Minimum Score เป็น `4.0`

## ข้อจำกัด

- ต้องใช้กับสินค้าที่มี volume จริง ผลจะแม่นขึ้น
- Tier 2/3 เป็น event เชิงอัตนัยและอาจมี false positive
- ยังไม่ได้ทดสอบ compile บน TradingView ในสภาพแวดล้อมนี้ — หากพบ error ให้ตรวจสอบข้อความแดงและเลขบรรทัด
