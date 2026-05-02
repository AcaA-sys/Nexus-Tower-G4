Work in Progress. 

# 🗼 NEXUS-TOWER v6.0 Final
> **High-Performance 6-Axis Stepper Controller based on STM32G431**


## 📋 Обзор проекта
**NEXUS-TOWER** — это специализированный контроллер для систем высокоточного перемещения (Pick-and-Place, роборуки), оптимизированный под совместную работу двигателей NEMA 11 и NEMA 17. Версия 6.0 получила продвинутую систему защиты питания и расширенную периферию.

---


## 🏎️ Управление движением
Контроллер управляет 6 осями с полной обратной связью по UART.

*   **Особенности**: 
    *   Поддержка `StealthChop2` для бесшумной работы.
    *   `StallGuard` для безсенсорного поиска дома.
    *   Разделение UART на две группы для повышения отказоустойчивости шины.

---

## 🔌 Периферия и Интерфейсы
*   **Vacuum Control**: 4 быстрых канала АЦП (фильтрация RC) для датчиков вакуумного захвата.
*   **Pneumatics**: 8 каналов управления клапанами через силовой массив `TD62083`.
*   **Expansion**: 14-pin FFC разъем (`Wurth 68611414122`) для подключения внешних модулей по **I2C**.

---

## 🛠️ Распиновка (Ключевые узлы)
```yaml
MCU: STM32G431RBT6 (LQFP64)
---------------------------
Brake Control:  PB0 (PWM)
Brake Monitor:  PB12 (ADC)
Status LEDs:    2 Channels
Expansion Port: I2C1

# Nexus-Tower-G4 (OpenPnP Head Controller)

Универсальный и высокопроизводительный контроллер «головы» установщика компонентов OpenPnP. Построен на базе экосистемы **Nexus-Drive-FD**.

## Технические характеристики
* **MCU:** STM32G431R (LQFP64) — Mixed-Signal Control с ускорителем CORDIC.
* **Шина:** CAN FD (Isolated) до 5 Mbps (Трансивер TD541S).
* **Драйверы:** 6x TMC2226/2225 (Step/Dir + UART Config).
* **Сенсоры:** 4x АЦП канала вакуума (ADS1115 на I2C), датчик вибрации (LIS3DH), термометр (DS18B20).

---

## Карта портов (Pinout)

### 1. Управление движением (6 осей)

| Ось | STEP (Port A) | DIR (Port C) | Примечание |
| :--- | :--- | :--- | :--- |
| **X1** | PA2 | PC2 | Скоростной блок Port A |
| **X2** | PA1 | PC0 | |
| **Z1** | PA0 | PC12 | |
| **Z2** | PA7 | PC15 | |
| **C1** | PA6 | PC3 | |
| **C2** | PA5 | PC1 | |
| **ALL** | **EN: PC13** | **DIAG: PA3** | Общий Enable и StallGuard |

### 2. Настройка драйверов (UART)
* **UART_1 (PC4/PC5):** Конфигурация осей 1, 2, 3.
* **UART_3 (PC10/PC11):** Конфигурация осей 4, 5, 6.

### 3. Периферия и Сенсоры
* **CAN FD:** PA11 (RX) / PA12 (TX)
* **I2C Bus (PC8/PC9):** ADS1115, AT24C32D, OLED 1.3", LIS3DH.
* **One-Wire (PA8):** DS18B20 (Термоконтроль).
* **Endstops:** PB4 (Z1), PB6 (Z2), PD2 (X), PB7 (3D-Touch).
* **Fan Control:** PB1 (PWM), PA15(Tacho).
* **EEPROM WP:** PB5 (Защита от записи).

### 4. Силовая часть (TD62083)
* **Клапаны 1-4:** PB15, PB14, PB13, PB12.
* **Клапаны 5-6:** PC7, PC6.
* **Light:** PA4 (PWM через CSD18543Q3A).
* **Brake FET:** PB0 (Brake FET через CSD18543Q3A).
* **Monitoring:** PB2 (24V Check / ADC).

### 5. Индикация и Сервис
* **LED Status:** PB9 (Встречно-параллельные диоды / Режим High-Z).
* **Service Port:** PB10, PB11 (LPUART1).
* **Board ID:** PC14.


