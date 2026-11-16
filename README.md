# Project : ESP32 Laboratory with ESP-IDF

<p align="center">
  <b>Microprocessor & Embedded Systems Labs</b><br>
  รวมแบบฝึกหัด ESP32 สำหรับศึกษาระบบสมองกลฝังตัว การเชื่อมต่ออุปกรณ์ และการทำงานหลาย Task
</p>

---

## About Project

Repository นี้รวบรวมงานห้องปฏิบัติการจากรายวิชาด้านไมโครโพรเซสเซอร์ อิเล็กทรอนิกส์ และระบบสมองกลฝังตัว โดยเขียนโปรแกรมภาษา C บน ESP32 ผ่าน ESP-IDF

แต่ละโฟลเดอร์เป็นการทดลองแยกหัวข้อ ตั้งแต่การแสดงข้อความผ่าน Serial การอ่านและควบคุมขา GPIO ไปจนถึง UART, PWM, ADC, FreeRTOS และการเชื่อมต่อเครือข่ายด้วย Wi-Fi และ MQTT จึงสามารถเลือกศึกษาและทดลองเป็นราย Lab ได้

ภายใน repository ยังมีเอกสารประกอบการเรียน PDF สำหรับบางบท เพื่อใช้อ่านร่วมกับโค้ดและการต่อวงจรจริง

---

## Laboratory Contents

| โฟลเดอร์ | หัวข้อการทดลอง | สิ่งที่ศึกษา |
|---|---|---|
| `Lab2` | โปรแกรมเริ่มต้น | ใช้ `app_main()` และแสดงข้อความด้วย `printf()` |
| `Lab5` | GPIO | กำหนด Input/Output, อ่านค่าแบบ Polling และรับ Interrupt ผ่าน Queue |
| `Lab6` | UART | กำหนดพอร์ต ขา TX/RX และ Baud Rate พร้อมตัวอย่างส่งและอ่านข้อมูล |
| `Lab7` | Servo PWM | ใช้ MCPWM สร้างสัญญาณควบคุม Servo และปรับมุมตามลำดับ |
| `Lab7n` | Software Timer | ใช้ `esp_timer` สลับสถานะ LED ที่ GPIO 13 เป็นคาบ |
| `Lab8` | Analog Input | อ่านค่า ADC แบบ One-shot จาก ADC1 สอง Channel |
| `Lab9n1` | FreeRTOS Queue | ส่งค่าระหว่าง Producer Task และ Consumer Task |
| `Lab9n2` | FreeRTOS Mutex | ให้หลาย Task ใช้งานส่วนแสดงผลร่วมกันผ่าน Mutex |
| `Lab11` | Wi-Fi & MQTT | เชื่อมต่อ Wi-Fi แบบ Station และทดลอง Publish/Subscribe กับ MQTT Broker |

ไฟล์ `Lab1.txt` เป็นไฟล์ว่างที่เก็บไว้ใน repository ส่วนตัวอย่างที่มีโค้ดการทดลองเริ่มอยู่ในโฟลเดอร์ Lab ตามตาราง

---

## Features

### Hardware Interfaces

- กำหนดโหมดและสถานะของ GPIO
- ใช้ Pull-up และตรวจจับสัญญาณขอบขาลงสำหรับ Interrupt
- สื่อสารผ่าน UART โดยกำหนดค่าจาก Project Configuration
- สร้าง PWM สำหรับทดลองควบคุม Servo
- อ่านค่าดิบของสัญญาณ Analog ผ่าน ADC

### Real-time Programming

- สร้าง FreeRTOS Task และกำหนด Priority
- ส่งข้อมูลระหว่าง Task ด้วย Queue
- ใช้ Mutex ควบคุมการเข้าถึงทรัพยากรร่วมกัน
- เรียก Callback เป็นคาบด้วย `esp_timer`

### Networking

- เชื่อมต่อ Wi-Fi ในโหมด Station
- รับเหตุการณ์เชื่อมต่อ หลุดการเชื่อมต่อ และได้รับ IP Address
- เชื่อมต่อ MQTT Broker ตามค่าที่กำหนด
- ทดลองส่งข้อความ สมัครรับ Topic และแสดงข้อความที่ได้รับผ่าน Serial Log

---

## Project Structure

```text
LabIDF_by-Esp32/
├── Lab2/
├── Lab5/
├── Lab6/
├── Lab7/
├── Lab7n/
├── Lab8/
├── Lab9n1/
├── Lab9n2/
├── Lab11/
│   ├── main/
│   │   ├── Lab11.c       # เริ่มระบบและเชื่อมต่อ Wi-Fi
│   │   ├── mqtt.c        # MQTT Client และ Event Handler
│   │   └── Kconfig.projbuild
│   └── CMakeLists.txt
└── เอกสารประกอบการเรียน/
```

แต่ละ Lab มี `CMakeLists.txt` และโฟลเดอร์ `main` ของตนเอง ส่วนบาง Lab มี `Kconfig.projbuild` สำหรับเพิ่มตัวเลือกในเมนูตั้งค่า

---

## Technology Stack

- ESP32
- C
- ESP-IDF
- FreeRTOS
- CMake
- GPIO, UART, MCPWM และ ADC Drivers
- Wi-Fi และ MQTT
- ESP Logging และ Serial Monitor

---

## Getting Started

เตรียมบอร์ด ESP32 สาย USB สำหรับรับส่งข้อมูล และ ESP-IDF พร้อม Toolchain ในเครื่อง จากนั้นเปิด Terminal ที่โหลด ESP-IDF Environment แล้วเลือกเข้าโฟลเดอร์ Lab ที่ต้องการ เช่น:

```bash
git clone https://github.com/kittanai46/LabIDF_by-Esp32.git
cd LabIDF_by-Esp32/Lab11
idf.py set-target esp32
idf.py menuconfig
idf.py build
```

สำหรับ Lab11 ให้ตั้งค่า Wi-Fi และ MQTT Broker ผ่านเมนูของโปรเจกต์ก่อน Build จากนั้น Flash และดู Log โดยแทน `<PORT>` ด้วยพอร์ตของบอร์ดจริง:

```bash
idf.py -p <PORT> flash monitor
```

สำหรับ Lab ที่ใช้ GPIO, UART, Servo หรือ ADC ให้ตรวจสอบหมายเลขขาในไฟล์ `.c` และค่าของ Project Configuration ก่อนต่ออุปกรณ์ เพราะแต่ละ Lab ใช้การตั้งค่าและวงจรต่างกัน

---

## Project Notes

- แต่ละ Lab เป็นตัวอย่างแยกกัน ควร Build และ Flash จากโฟลเดอร์ของ Lab นั้น
- Lab7 กำหนดสัญญาณ Servo ที่ GPIO 13 ส่วน Lab7n ใช้ GPIO 13 สำหรับ LED แต่เป็นคนละโปรเจกต์
- ตัวอย่างอ้างอิง ESP-IDF Driver API เช่น `mcpwm_prelude` และ `adc_oneshot` จึงต้องใช้ ESP-IDF รุ่นที่รองรับ API เหล่านี้
- ไฟล์ Build และการตั้งค่าบางส่วนจากเครื่องเดิมถูกเก็บอยู่ใน repository ควรสร้าง Build ใหม่ให้ตรงกับ Environment ของตนเอง
- ผลการทดลองขึ้นกับบอร์ด การต่อวงจร และอุปกรณ์ที่ใช้ README นี้อธิบายจากซอร์สโค้ดและยังไม่ได้ยืนยันผลบนฮาร์ดแวร์จริง

---

## Repository Owner

[Kittanai Srikham](https://github.com/kittanai46)

