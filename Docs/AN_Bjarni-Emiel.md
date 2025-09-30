# Application Note — Sensor Module

## 1. Doel
Deze module is bedoeld om **temperatuur** en **luchtvochtigheid** te meten in spouwmuren en deze data draadloos door te sturen voor ecologisch en bouwkundig onderzoek.

## 2. Achtergrond
Om vleermuizen effectief te beschermen en hun gedrag te begrijpen, is het essentieel om omgevingsfactoren zoals temperatuur en luchtvochtigheid te monitoren. Lange termijnmetingen zijn nodig voor betrouwbare data.

## 3. Hardwarecomponenten
- **ESP32-S2 Mini** — microcontroller met ingebouwde Wi-Fi.  
- **SHT30 sensor** — nauwkeurige temperatuur- en luchtvochtigheidsmeting.  
- **PowerBoost 500 Charger** — batterijvoeding en opladen.  
- **LiPo batterij** — 2000–5000 mAh voor autonome werking.

## 4. Systeemarchitectuur
1. **Meten:** periodieke uitlezing van sensorwaarden.  
2. **Opslaan:** lokaal buffer in EEPROM/microSD.  
3. **Doorsturen:** Wi-Fi naar server of MQTT-broker.  
4. **Beheren:** configuratie via software of op afstand.

## 5. Communicatieprotocol
- JSON payload, bijvoorbeeld:  
```json
{
  "device_id": "esp32-01",
  "timestamp": 1696070400000,
  "temperature": 18.4,
  "humidity": 72.3
}
```
- MQTT-topic: vleermuis/sensors
- HTTP-endpoint: /api/sensors (optioneel)

## 6. Energiebeheer
- Deep-sleep modus minimaliseert verbruik.
- Wake-up interval: 1–5 minuten.
- Batterijduur: 3–14 dagen afhankelijk van configuratie.

## 7. Omgevingsbescherming
- Behuizing: spatwaterdicht (IP54+).
- Condensbescherming: silica-gel of ventilerende membranen.

## 8. Mogelijke uitbreidingen
- Bewegingssensor (PIR/ultrasoon) voor activiteitdetectie.
- Ultrasone microfoon voor vleermuisgeluid.
- PCB voor compactere modules.
- Cloud-integratie (Grafana/InfluxDB) voor analyse.

9. Conclusie
Met deze module kunnen duurzame en nauwkeurige omgevingsmetingen worden uitgevoerd in spouwmuren, wat ecologisch onderzoek en diervriendelijke renovaties ondersteunt.
