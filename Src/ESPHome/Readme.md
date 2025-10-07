# ESPHome Web / ESPHome Web Tools — Overzicht & Documentatie

## Inleiding

ESPHome is een open-source firmwareframework dat het eenvoudiger maakt om aangepaste firmware te laten draaien op WiFi-microcontrollers (zoals ESP32 of ESP8266) voor gebruik in domotica-omgevingen. ([esphome.io](https://esphome.io))  

**ESPHome Web / Web Tools** is een webgebaseerde interface waarmee je apparaten kunt voorbereiden, firmware kunt installeren, logs kunt bekijken, en instellingen kunt beheren via een browser. ([web.esphome.io](https://web.esphome.io))  

---

## Features & functionaliteit

| Feature | Beschrijving |
|---|---|
| **Apparaatvoorbereiding / eerste gebruik** | Via de browser kun je een apparaat “klaarmaken voor eerste gebruik” (bijv. wifi-configuratie, initialisatie). |
| **Firmware-installatie / updates** | Je kunt nieuwe versies van firmware naar het apparaat sturen via de browserinterface (met ondersteuning voor identificatie van het board). |
| **Logweergave & console** | Logs van het apparaat kunnen live getoond worden via de webinterface; je kunt ook commando’s via de console sturen. |
| **Web‑server integratie op het apparaat** | Het apparaat zelf draait een eenvoudige webserver met toegang tot een front-end, REST API en event‑streaming. |
| **REST API & Event Source** | Je kunt componentstatussen opvragen via GET-verzoeken, en real-time updates ontvangen via server-sent events (SSE) via `/events`. |
| **Ondersteuning voor meerdere componenten** | De REST API ondersteunt componenttypes als `sensor`, `switch`, `light`, `cover`, `fan`, `select`, `number`, `button`, `alarm_control_panel`, etc. |

---

## Architectuur & technische details

### Web Tools & manifest

- ESP Web Tools maakt gebruik van **Web Serial**, **Improv Wi-Fi** (optioneel) en een manifestbestand dat beschrijft welke firmwarevariant voor welk apparaat gebruikt moet worden.  
- Het manifest (JSON) bevat velden als `name`, `version`, `builds` (met `chipFamily`, `parts`, etc.), en optionele velden zoals `funding_url`, `new_install_prompt_erase`, enz.  
- Voor ESP32 kan het nodig zijn om firmware-images samen te voegen tot één binair bestand, zodat Web Tools ze correct kan flashen.  
- Voor integratie op je eigen website kun je de `<esp-web-install-button>` tag gebruiken, waarbij je een manifestbestand verwijst via de `manifest`-attribuut.  

### Web‑server op het apparaat

- In je ESPHome-configuratie kun je de webserver inschakelen via `App.init_web_server()` of via de web_server-component.  
- De webserver biedt:
  1. Een webfrontend (via root `/`)  
  2. Een REST-API (GET/POST) voor componentstatussen en controle  
  3. Een event‑source‑interface (`/events`) voor real-time updates  
- De REST API volgt in grote lijnen het pad `/<domain>/<id>[/<method>?<param>=<value>]`. Bijvoorbeeld `/light/lamp1/turn_on?brightness=128`.  
- Voor componentstatus opvragen: GET op `/sensor/<id>`, `/switch/<id>`, etc.  
- Voor acties: POST-verzoeken zoals `/switch/my_switch/turn_on`, `/cover/front_blinds/set?position=0.5`, etc.  

---

## Voorbeeld van REST API gebruik

### Sensor status opvragen  
```http
GET /sensor/outside_temperature
Response: {
  "id": "sensor-outside_temperature",
  "state": "19.8 °C",
  "value": 19.76666
}
```

### Switch inschakelen  
```http
POST /switch/dehumidifier/turn_on
```

### Light aanzetten met helderheid  
```http
POST /light/living_room_lights/turn_on?brightness=128&transition=2
```

### Cover gedeeltelijk instellen  
```http
POST /cover/front_window_blinds/set?position=0.1&tilt=0.3
```

---

## Hoe beginnen

1. Ga naar de ESPHome Web interface via je browser (via het IP-adres van je apparaat of via mDNS zoals `naam.local/`).  
2. Gebruik de Web Tools interface om je apparaat te “prepareren voor eerste gebruik” (wifi-instellingen, initialisatie).  
3. Installeer de firmware via de browser (via Web Serial / Web Tools).  
4. Activeer de webservercomponent in je YAML / code zodat je via de webinterface en API toegang hebt tot status en commando’s.  
5. Gebruik de REST API of event source voor integratie met andere systemen of eigen frontend.

---

**Bronnen:**  
- [ESPHome Web API Documentatie](https://esphome.io/web-api/)  
- [ESPHome Web Tools](https://esphome.github.io/esp-web-tools/)  
- [ESPHome Hoofdpagina](https://esphome.io/)  
