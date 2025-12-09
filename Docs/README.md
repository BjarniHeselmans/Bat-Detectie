Deze map bevat alle documentatie die is opgesteld tijdens het **Bat Detectie**-project.  
Hieronder volgt een overzicht van de bestanden en hun inhoud.

---

## Documenten

### 1. [Research.md](./Research.md)
**Onderwerp:** Hardware overzicht en functionaliteit.  
**Inhoud:**  
- Beschrijving van de **S2 Mini**, **PowerBoost 500 Charger** en **SHT30-sensor**.  
- Functionele uitleg van voeding, opladen en datalogging.  
- Aansluitingen en pinout details.  
- Toepassingen, tips en referenties naar datasheets en documentatie.

---

### 2. [Board_controle.md](./Board_controle.md)
**Onderwerp:** Controle van de S2 Mini-boardjes.  
**Inhoud:**  
- Testen van de boardjes via **Arduino IDE** en seriële monitor.  
- Identificatie van werkende en defecte boardjes.  
- Nummering en registratie voor verdere verwerking.  
- Screenshot van de seriële monitoruitvoer: `./Attachments/serial_monitor_output.png`.

---

### 3. [Sensor_kabels.md](./Sensor_kabels.md)
**Onderwerp:** Verkorten en aansluiten van SHT3X-sensorbekabeling.  
**Inhoud:**  
- Controle op schade en waterschade.  
- Verkorten van kabels tot 1 meter voor betrouwbare I²C-communicatie.  
- Correcte aansluiting volgens datasheet.  
- Foto van sensor met kabel: `./Attachments/SensorCable.png`.

---

### 4. [S2mini_flashen.md](./S2mini_flashen.md)
**Onderwerp:** Flashen van de S2 Mini met ESPHome.  
**Inhoud:**  
- Installatie van ESPHome via pip.  
- Flashen met `esphome run .` en testen via `esphome logs .`.  
- YAML-configuratie voor de sensor, Wi-Fi, deep sleep en logging.  
- Gemaakt in samenwerking met Alexander (junior onderzoeker).

---

### 5. [ErrorGuide.md](./ErrorGuide.md)
**Onderwerp:** Guide to fix the commen error to be unable to flash.  
**Inhoud:**  
- een step by step guide om de error te kunnen oplossen
- vervolgt met de mannier om de esp te flashen

### 6. [HWInstallationGuide.md](./HWInstallationGuide.md)
**Onderwerp:** Hardware assembly guide for the casing.  
**Inhoud:**  
- een step by step guide om de casing in elkaar te steken

---

## Bijlagen

- **Attachments/**  
  Bevat afbeeldingen ter ondersteuning van de documentatie:

---
