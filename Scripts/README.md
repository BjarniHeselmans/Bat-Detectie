# ESPHome Sensor Node – Gebruik en Flashen

Deze sectie legt uit hoe de ESPHome-configuratie voor de sensor node werkt
en hoe je de firmware flasht op de **S2 Mini (ESP32-S2)** binnen dit project.

---

## 1. Wat doet deze ESPHome-config?

De ESPHome-configuratie voor deze node zorgt ervoor dat de S2 Mini:

- verbinding maakt met Wi‑Fi;
- de **SHT30/SHT3X-sensor** via I²C uitleest;
- **temperatuur** en **luchtvochtigheid** als entiteiten beschikbaar maakt;
- (optioneel) **deep-sleep** gebruikt om batterij te besparen;
- OTA-updates en logging via ESPHome ondersteunt.

De belangrijkste configuratie staat in:

- `Scripts/device(NMR).yaml`

---

## 2. Bestanden en structuur

In deze repo:

- `Scripts/HTSensor.yaml`  
  ESPHome-configuratie voor de S2 Mini:
  - type bord (`esp32-s2` / S2 Mini)
  - Wi‑Fi-instellingen
  - SHT30/SHT3X-sensor (I²C)
  - logger, API, OTA, deep-sleep (indien geconfigureerd)

- `Docs/03_s2mini_flashen.md`  
  Stapsgewijze uitleg om de S2 Mini te flashen (achtergrond en screenshots).

---

## 3. Voorbereiding

1. **Benodigdheden**
   - S2 Mini (ESP32-S2)
   - SHT30/SHT3X-sensor correct aangesloten (zie `Docs/02_sensor_kabels.md`)
   - USB‑kabel naar je pc
   - Wi‑Fi-netwerk (SSID + wachtwoord)

2. **Software**
   - Python + `pip`
   - ESPHome installeren:
     ```
     pip install esphome
     ```
   - Optioneel: ESPHome Dashboard (via Home Assistant of standalone)

---

## 4. Wi‑Fi en sensorgegevens instellen

Open `Scripts/HTSensor.yaml` en controleer:

- **Wi‑Fi-instellingen**:
wifi:
ssid: "JOUW_SSID"
password: "JOUW_WACHTWOORD"

- **Sensorconfiguratie** (voorbeeld):
i2c:
sda: <GPIO_SDA>
scl: <GPIO_SCL>
scan: true

sensor:
- platform: sht3xd
temperature:
name: "Spouwmuur Temperature"
humidity:
name: "Spouwmuur Humidity"
address: 0x44
update_interval: 10s


Pas hier enkel aan wat in jouw opstelling afwijkt (SSID, wachtwoord, pinnen, namen).

---

## 5. Eerste keer flashen (via USB)

1. Verbind de S2 Mini via USB met je pc.
2. Ga in een terminal naar de projectmap:
cd Scripts

3. Flash de node met ESPHome:
esphome run HTSensor.yaml

4. Kies de juiste seriële poort wanneer ESPHome daarom vraagt.

ESPHome:
- compileert de firmware;
- uploadt ze naar de S2 Mini.

---

## 6. Logs bekijken en testen

Na het flashen kun je live logs bekijken:

esphome logs HTSensor.yaml

Controleer of:
- de node verbinding maakt met je Wi‑Fi;
- de SHT30/SHT3X-sensor waarden geeft;
- (indien ingesteld) deep-sleep correct werkt (node gaat slapen en wordt weer wakker).

---

## 7. OTA-updates (draadloos)

Na de eerste USB-flash kun je wijzigingen aan `HTSensor.yaml` draadloos uploaden:

esphome run HTSensor.yaml

ESPHome zoekt dan de node op je netwerk en doet een OTA-update.

---

## 8. Integratie in het BatSense-systeem

De sensoren die in `HTSensor.yaml` gedefinieerd zijn (bijv. `Spouwmuur Temperature`,
`Spouwmuur Humidity`) verschijnen als entiteiten in ESPHome / Home Assistant
of kunnen door de centrale BatSense-componenten uitgelezen worden volgens de
architectuur die in het teamproject is afgesproken.

---

## 9. Veelvoorkomende problemen

- **Node verschijnt niet op Wi‑Fi**  
  → Controleer SSID/wachtwoord in `HTSensor.yaml`.  
- **Geen sensorwaarden**  
  → Controleer I²C-pinnen en bekabeling (zie `Docs/02_sensor_kabels.md`).  
- **Geen logs**  
  → Controleer seriële poort of netwerk, probeer opnieuw:
    ```
    esphome logs HTSensor.yaml
    ```
