# S2 Mini & PowerBoost 500 Charger & SHT30

Dit project combineert de **S2 Mini** microcontroller met de **Adafruit PowerBoost 500 Charger** en de **SHT30 temperatuur- en vochtigheidssensor** voor een compacte, draagbare oplossing die zowel voeding, opladen als omgevingsmeting ondersteunt.

## Componenten

- **S2 Mini**
  - ESP32-S2 gebaseerde microcontroller
  - Ondersteunt Wi-Fi
  - Klein formaat en laag energieverbruik

- **PowerBoost 500 Charger**
  - LiPo/Li-ion batterij lader
  - 5V boost converter tot max. 500mA
  - Micro-USB aansluiting voor opladen
  - Automatische overschakeling tussen USB- en batterijvoeding

- **SHT30**
  - Temperatuur- en luchtvochtigheidssensor
  - Meetbereik:
    - Temperatuur: -40 tot +125 °C (±0.2 °C nauwkeurigheid)
    - Vochtigheid: 0–100 %RH (±2 %RH nauwkeurigheid)
  - Communicatie via I²C
  - Lage stroomconsumptie, geschikt voor draagbare toepassingen

## Functionaliteit

- Voeding van de **S2 Mini** via een LiPo- of Li-ion batterij.
- Opladen van de batterij via micro-USB.
- 5V output van de PowerBoost voedt direct de S2 Mini.
- Metingen van temperatuur en luchtvochtigheid via de SHT30.
- Data kan via Wi-Fi worden doorgestuurd of lokaal verwerkt.
- Ideaal voor draagbare IoT-projecten en omgevingsmonitoring.

## Aansluitingen
<img width="2480" height="1642" alt="image" src="https://github.com/OliwierJaworski/Bat-Detectie/blob/main/Docs/Attachments/Volledige_Opstelling.png" />
1. **Batterij → PowerBoost**
   - Verbind een LiPo/Li-ion batterij met de JST-connector van de PowerBoost.

2. **PowerBoost → S2 Mini**
   - Sluit de **5V-uitgang** van de PowerBoost aan op de **5V/VBUS pin** van de S2 Mini.
   - Sluit **GND** van beide borden aan.

3. **SHT30 → S2 Mini**
   - **VCC** → 3.3V pin van de S2 Mini  
   - **GND** → GND van de S2 Mini  
   - **SDA** → GPIO 8 (SDA)  
   - **SCL** → GPIO 9 (SCL)  
   *(controleer de pinout van je S2 Mini, sommige boards gebruiken andere standaard I²C-pinnen)*

4. **Opladen**
   - Gebruik een micro-USB kabel op de PowerBoost om de batterij op te laden.
   - Het systeem kan tijdens het opladen blijven functioneren.

## Let op

- Zorg dat de aangesloten batterij correct gepolariseerd is (rode draad = +, zwarte draad = -).
- De PowerBoost levert max. 500mA; houd rekening met stroomverbruik van de S2 Mini, SHT30 en eventuele extra randapparatuur.
- De SHT30 werkt op 3.3V; sluit hem niet aan op 5V.
- Gebruik een geschikte LiPo- of Li-ion batterij (bij voorkeur ≥ 500mAh).

## Toepassingen

- Draagbare IoT-projecten
- Sensoren en datalogging
- Omgevingsmonitoring (temperatuur en luchtvochtigheid)
- Kleine robotica toepassingen
- Wearables

## Referenties

- [S2 Mini documentatie](https://www.wemos.cc/en/latest/s2/s2_mini.html)  
- [Adafruit PowerBoost 500 Charger](https://cdn-learn.adafruit.com/downloads/pdf/adafruit-powerboost-500-plus-charger.pdf)  
- [SHT30 Datasheet (Sensirion)](https://sensirion.com/media/documents/213E6A3B/63A5A569/Datasheet_SHT3x_DIS.pdf)
- [SHT3x module functionality(controllerstech)](https://controllerstech.com/interface-sht3x-with-arduino/)