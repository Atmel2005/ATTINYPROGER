# Universal AVR Programmer PRO (TPI, UPDI, ISP, HVSP & 12V Rescue)

## Deutsch

Das Projekt ist ein universeller Hochgeschwindigkeits-Programmierer und Hardware-Reanimator für Atmel/Microchip AVR-Mikrocontroller auf Basis eines Arduino UNO oder Nano. Die Steuerungssoftware ist in Rust mit egui geschrieben, arbeitet als eigenständige `.exe`-Datei ohne externe Abhängigkeiten und unterstützt Standard-5V sowie 12V-Hochvolt-Reanimation für TPI, UPDI, ISP und HVSP.

### Ausrüstung

- Arduino UNO oder Nano (ATmega328P)
- Optokoppler PC817 + Diode 1N4148 (12V HV-Impulstor)
- 4× 100 nF Kondensatoren + 4× 1N4148 Dioden (integrierte Dickson-12V-Ladungspumpe)
- 1× 4.7 kΩ Widerstand (UPDI-Strombegrenzung), 1× 330 Ω (PC817 Vorwiderstand)
- 1× PNP-Transistor (Target VCC Ein-/Ausschaltung)
- Ziel-Mikrocontroller (ATtiny, ATmega)

### Verdrahtung

Arduino bietet zwei wählbare Pin-Belegungen (Standard und Alternative):

| Signal / Funktion | Arduino Pin (Standard) | Arduino Pin (Alternativ) | Ziel-Mikrocontroller |
| --- | --- | --- | --- |
| MOSI / SDI / TPIDATA | D11 | D4 | TPI: Pin 1 / ISP: MOSI / HVSP: SDI |
| MISO / SDO | D12 | D5 | ISP: MISO / HVSP: SDO |
| SCK / SCI / TPICLK | D13 | D6 | TPI: Pin 3 / ISP: SCK / HVSP: SCI |
| UPDI / 5V Target Reset | D8 | D8 | UPDI: Pin 6 (über 4.7 kΩ) |
| 12V HV Gate | D7 | D7 | An Optokoppler PC817 |
| 12V Dickson Pump (62.5 kHz) | D9, D10 | D9, D10 | An Dioden-Kondensator-Kaskade |
| 1.0 MHz Rescue Clock | D3 | D3 | An XTAL1 des Zielchips |
| Dedicated ISP Reset | A4 | A4 | An RESET bei klassischem ISP |
| Target VCC Switch | A5 | A5 | An Basis des PNP-Transistors |
| Versorgung | +5V / GND | +5V / GND | VCC und GND des Zielchips |

> Die Umschaltung zwischen Standard (D11–D13) und Alternative (D4–D6) erfolgt live im Programm-Interface und wird hardwareseitig sofort in der Arduino-Firmware umgeschaltet.

### Hauptfunktionen

- Vier Schnittstellen in einem Gerät: TPI, UPDI, ISP und HVSP
- Autonome 12V-Erzeugung über Hardware-Timer1 (62.5 kHz Gegentakt) ohne externes Netzteil
- Hardware-Rettungstakt (1.0 MHz Rechtecksignal an D3 via Timer2) zur Wiederbelebung von Chips mit verstellten Clock-Fuses
- Integrierter STK500v1-Flasher: Überträgt die Arduino-Firmware mit einem Klick direkt aus dem GUI
- Interaktiver Fuse-Manager (Fuse X) mit Bitfeld-Editor und Voreinstellungen
- HEX-Viewer mit Diff-Funktion zum schnellen Vergleich von Puffer und Flash-Speicher
- Vollkommen eigenständige Windows `.exe` ohne Python- oder AVRDUDE-Installationsbedarf

### Unterstützte Chips und Modi

- **TPI (5V & 12V HV):** ATtiny4, ATtiny5, ATtiny9, ATtiny10, ATtiny20, ATtiny40 (inklusive Entsperrung von `RSTDISBL`).
- **UPDI (5V & 12V HV):** tinyAVR 0/1/2-Serie (ATtiny202, 402, 412, 814, 1614, 3216 usw.) mit Reaktivierung als GPIO konfigurierter Pins.
- **Classic ISP (5V):** ATmega8, 16, 32, 48, 88, 168, 328P, ATtiny24, 44, 84, 2313 usw. (mit Rescue Clock an XTAL1).
- **HVSP (12V HV):** ATtiny13, ATtiny25, ATtiny45, ATtiny85 (Rettung bei deaktiviertem RESET).

### Nutzung

1. Verbinde den Arduino UNO / Nano per USB mit dem PC.
2. Starte `ATtinyProger.exe`. Wähle bei Bedarf den Menüpunkt `⚡ Flash Arduino`, um die Firmware automatisch aufzuspielen.
3. Wähle im Hauptfenster den COM-Port und den gewünschten Zielchip aus.
4. Schließe den Ziel-Mikrocontroller gemäß Schaltplan an.
5. Klicke auf `Connect` / `Detect Chip`, lies die Fuses aus, lade eine `.hex`-Datei und führe `Write Flash` oder `Chip Erase` aus.

---

## Українська

Проєкт є універсальним швидкісним програматором та апаратним реаніматором мікроконтролерів Atmel/Microchip AVR на базі плати Arduino UNO або Nano. Керуюча програма написана на Rust з графічним інтерфейсом egui, працює як єдиний `.exe`-файл без сторонніх залежностей та підтримує стандартне 5В програмування і 12В високовольтне відновлення для TPI, UPDI, ISP та HVSP.

### Обладнання

- Arduino UNO або Nano (ATmega328P)
- Оптопара PC817 + діод 1N4148 (комутація імпульсу 12В)
- 4× конденсатори 100 нФ + 4× діоди 1N4148 (вбудований помножувач Діксона 12В)
- 1× резистор 4.7 кОм (захист лінії UPDI), 1× 330 Ом (струмообмежувач PC817)
- 1× PNP-транзистор (комутація живлення Target VCC)
- Цільовий мікроконтролер (ATtiny, ATmega)

### Підключення

Arduino підтримує два варіанти призначення виводів (Стандартний та Альтернативний):

| Сигнал / Функція | Вивід Arduino (Стандарт) | Вивід Arduino (Альтернатива) | Цільовий мікроконтролер |
| --- | --- | --- | --- |
| MOSI / SDI / TPIDATA | D11 | D4 | TPI: Pin 1 / ISP: MOSI / HVSP: SDI |
| MISO / SDO | D12 | D5 | ISP: MISO / HVSP: SDO |
| SCK / SCI / TPICLK | D13 | D6 | TPI: Pin 3 / ISP: SCK / HVSP: SCI |
| UPDI / 5V Target Reset | D8 | D8 | UPDI: Pin 6 (через 4.7 кОм) |
| 12V HV Gate | D7 | D7 | На оптопару PC817 |
| 12V Dickson Pump (62.5 кГц) | D9, D10 | D9, D10 | До каскаду конденсаторів та діодів |
| 1.0 МГц Rescue Clock | D3 | D3 | До виводу XTAL1 чипа |
| Dedicated ISP Reset | A4 | A4 | До RESET при звичайному ISP |
| Target VCC Switch | A5 | A5 | До бази PNP-транзистора |
| Живлення | +5V / GND | +5V / GND | VCC та GND цільового чипа |

> Перемикання між стандартом (D11–D13) та альтернативою (D4–D6) виконується на льоту у вікні схеми інтерфейсу та миттєво апаратно застосовується в прошивці Arduino.

### Основні можливості

- Чотири протоколи в одному пристрої: TPI, UPDI, ISP та HVSP
- Автономна генерація 12В через апаратний Timer1 (62.5 кГц push-pull) без зовнішнього блока живлення
- Апаратний тактовий генератор відновлення (1.0 МГц меандр на D3 через Timer2) для запуску чипів із заблокованим тактуванням
- Вбудований STK500v1 прошивальник Arduino: запис прошивки в плату в один клік прямо з GUI
- Інтерактивний менеджер ф'юзів (Fuse X) з бітовим редактором та готовими пресетами
- Вбудований HEX-переглядач з підсвіткою різниці (Diff) між файлом та пам'яттю чипа
- Автономний Windows `.exe` файл, який не потребує встановлення Python чи AVRDUDE

### Підтримувані чипи та режими

- **TPI (5В та 12В HV):** ATtiny4, ATtiny5, ATtiny9, ATtiny10, ATtiny20, ATtiny40 (включно з розблокуванням `RSTDISBL`).
- **UPDI (5В та 12В HV):** серія tinyAVR 0/1/2 (ATtiny202, 402, 412, 814, 1614, 3216 тощо) з відновленням режиму UPDI при налаштуванні піна як GPIO.
- **Classic ISP (5В):** ATmega8, 16, 32, 48, 88, 168, 328P, ATtiny24, 44, 84, 2313 тощо (з подачею тактового сигналу на XTAL1).
- **HVSP (12В HV):** ATtiny13, ATtiny25, ATtiny45, ATtiny85 (відновлення заводських налаштувань при відключеному RESET).

### Використання

1. Підключіть Arduino UNO / Nano до комп'ютера по USB.
2. Запустіть `ATtinyProger.exe`. За потреби натисніть `⚡ Flash Arduino`, щоб автоматично прошити скетч у плату.
3. Оберіть у головному вікні COM-порт та потрібний мікроконтролер.
4. Підключіть цільовий мікроконтролер згідно зі схемою.
5. Натисніть `Connect` / `Detect Chip`, зчитайте ф'юзи, відкрийте `.hex`-файл та виконайте `Write Flash` або `Chip Erase`.

---

## English

The project is a high-speed universal programmer and hardware unbricker for Atmel/Microchip AVR microcontrollers powered by an Arduino UNO or Nano. The host GUI is written in Rust with egui, operates as a single standalone `.exe` without third-party dependencies, and provides standard 5V programming alongside 12V high-voltage rescue for TPI, UPDI, ISP, and HVSP.

### Hardware

- Arduino UNO or Nano (ATmega328P)
- Optocoupler PC817 + 1N4148 diode (12V HV pulse gate)
- 4× 100 nF capacitors + 4× 1N4148 diodes (onboard Dickson 12V charge pump)
- 1× 4.7 kΩ resistor (UPDI current limiting), 1× 330 Ω (PC817 base resistor)
- 1× PNP transistor (Target VCC power switching)
- Target microcontroller (ATtiny, ATmega)

### Wiring

The Arduino firmware supports two switchable pin configurations (Standard and Alternate):

| Signal / Function | Arduino Pin (Standard) | Arduino Pin (Alternate) | Target Microcontroller |
| --- | --- | --- | --- |
| MOSI / SDI / TPIDATA | D11 | D4 | TPI: Pin 1 / ISP: MOSI / HVSP: SDI |
| MISO / SDO | D12 | D5 | ISP: MISO / HVSP: SDO |
| SCK / SCI / TPICLK | D13 | D6 | TPI: Pin 3 / ISP: SCK / HVSP: SCI |
| UPDI / 5V Target Reset | D8 | D8 | UPDI: Pin 6 (via 4.7 kΩ) |
| 12V HV Gate | D7 | D7 | To PC817 optocoupler |
| 12V Dickson Pump (62.5 kHz) | D9, D10 | D9, D10 | To diode-capacitor multiplier ladder |
| 1.0 MHz Rescue Clock | D3 | D3 | To XTAL1 of target MCU |
| Dedicated ISP Reset | A4 | A4 | To RESET for classic ISP |
| Target VCC Switch | A5 | A5 | To base of PNP power switch |
| Power | +5V / GND | +5V / GND | Target MCU VCC & GND |

> Toggling between Standard (D11–D13) and Alternate (D4–D6) pins is performed live in the GUI and takes effect immediately in Arduino hardware.

### Key features

- Four programming interfaces in one device: TPI, UPDI, ISP, and HVSP
- Autonomous onboard 12V generation via hardware Timer1 (62.5 kHz push-pull) without external power supply
- Hardware rescue clock (1.0 MHz square wave on D3 via Timer2) to unbrick MCUs with misconfigured clock fuses
- Embedded STK500v1 Arduino flasher: Upload programmer firmware directly from the GUI with one click
- Interactive Fuse X manager with bitfield configuration and presets
- Built-in HEX viewer with memory diff comparison against target MCU flash
- Standalone Windows `.exe` binary requiring no Python, drivers, or AVRDUDE toolchain

### Supported Chips and Modes

- **TPI (5V & 12V HV):** ATtiny4, ATtiny5, ATtiny9, ATtiny10, ATtiny20, ATtiny40 (including `RSTDISBL` recovery).
- **UPDI (5V & 12V HV):** tinyAVR 0/1/2 series (ATtiny202, 402, 412, 814, 1614, 3216, etc.) with HV override when pin is set as GPIO.
- **Classic ISP (5V):** ATmega8, 16, 32, 48, 88, 168, 328P, ATtiny24, 44, 84, 2313, etc. (with Rescue Clock on XTAL1).
- **HVSP (12V HV):** ATtiny13, ATtiny25, ATtiny45, ATtiny85 (unbricking when RESET pin is disabled).

### Usage

1. Connect Arduino UNO / Nano to PC via USB.
2. Launch `ATtinyProger.exe`. If needed, click `⚡ Flash Arduino` to flash the sketch automatically.
3. Select your COM port and target chip from the main toolbar.
4. Wire target microcontroller according to schematic.
5. Click `Connect` / `Detect Chip`, inspect fuses, load `.hex` file, and proceed with `Write Flash` or `Chip Erase`.

---

## Русский

Проект представляет собой универсальный скоростной программатор и аппаратный реаниматор микроконтроллеров Atmel/Microchip AVR на базе платы Arduino UNO или Nano. Графическая оболочка написана на Rust с библиотекой egui, работает в виде единого автономного `.exe`-файла без внешних зависимостей и обеспечивает как стандартное 5В программирование, так и 12В высоковольтное восстановление для TPI, UPDI, ISP и HVSP.

### Аппаратная часть

- Arduino UNO или Nano (ATmega328P)
- Оптопара PC817 + диод 1N4148 (ключ высоковольтного 12В импульса)
- 4× конденсатора 100 нФ + 4× диода 1N4148 (встроенный умножитель Диксона 12В)
- 1× резистор 4.7 кОм (ограничение тока UPDI), 1× 330 Ом (базовый резистор PC817)
- 1× PNP-транзистор (коммутация питания Target VCC)
- Прошиваемый микроконтроллер (ATtiny, ATmega)

### Подключение

Arduino поддерживает два варианта назначения выводов (Стандартный и Альтернативный):

| Сигнал / Функция | Вывод Arduino (Стандарт) | Вывод Arduino (Альтернатива) | Целевой микроконтроллер |
| --- | --- | --- | --- |
| MOSI / SDI / TPIDATA | D11 | D4 | TPI: Pin 1 / ISP: MOSI / HVSP: SDI |
| MISO / SDO | D12 | D5 | ISP: MISO / HVSP: SDO |
| SCK / SCI / TPICLK | D13 | D6 | TPI: Pin 3 / ISP: SCK / HVSP: SCI |
| UPDI / 5V Target Reset | D8 | D8 | UPDI: Pin 6 (через 4.7 кОм) |
| 12V HV Gate | D7 | D7 | На оптопару PC817 |
| 12V Dickson Pump (62.5 кГц) | D9, D10 | D9, D10 | К диодно-конденсаторному умножителю |
| 1.0 МГц Rescue Clock | D3 | D3 | К ножке XTAL1 чипа |
| Dedicated ISP Reset | A4 | A4 | К ножке RESET при классическом ISP |
| Target VCC Switch | A5 | A5 | К базе PNP-транзистора питания |
| Питание | +5V / GND | +5V / GND | VCC и GND целевого чипа |

> Переключение между стандартом (D11–D13) и альтернативой (D4–D6) осуществляется прямо в окне схемы в реальном времени и сразу аппаратно переназначается в прошивке Arduino.

### Основные возможности

- Четыре интерфейса в одном устройстве: TPI, UPDI, ISP и HVSP
- Автономная генерация 12В аппаратным Timer1 (двухтактный ШИМ 62.5 кГц) без внешнего блока питания
- Аппаратный тактовый генератор (1.0 МГц меандр на D3 через Timer2) для оживления чипов с заблокированными тактовыми фьюзами
- Встроенный STK500v1 прошивальщик Arduino: заливка прошивки в плату в 1 клик прямо из графического интерфейса
- Интерактивный редактор фьюзов (Fuse X) с битовой конфигурацией и готовыми пресетами
- Встроенный HEX-просмотрщик с подсветкой различий (Diff) между прошивкой и дампом чипа
- Автономный Windows `.exe` файл без необходимости установки Python или пакета AVRDUDE

### Поддерживаемые чипы и режимы

- **TPI (5В и 12В HV):** ATtiny4, ATtiny5, ATtiny9, ATtiny10, ATtiny20, ATtiny40 (включая снятие блокировки `RSTDISBL`).
- **UPDI (5В и 12В HV):** серия tinyAVR 0/1/2 (ATtiny202, 402, 412, 814, 1614, 3216 и др.) с разблокировкой ножки, настроенной как GPIO.
- **Classic ISP (5В):** ATmega8, 16, 32, 48, 88, 168, 328P, ATtiny24, 44, 84, 2313 и др. (с подачей частоты на XTAL1).
- **HVSP (12В HV):** ATtiny13, ATtiny25, ATtiny45, ATtiny85 (реанимация при отключенном RESET).

### Использование

1. Подключите Arduino UNO / Nano к компьютеру по USB.
2. Запустите `ATtinyProger.exe`. При необходимости нажмите `⚡ Flash Arduino`, чтобы автоматически залить скетч в плату.
3. Выберите в панели COM-порт и целевой микроконтроллер.
4. Подключите целевой чип согласно схеме.
5. Нажмите `Connect` / `Detect Chip`, проверьте фьюзы, откройте `.hex`-файл и нажмите `Write Flash` или `Chip Erase`.
