# Onderzoeksproject: Vleermuizen en Spouwmuren – Sensor Node (ESPHome)

<img width="2480" height="1642" alt="image" src="https://github.com/BjarniHeselmans/Bat-Detectie/blob/main/Docs/Attachments/ProjectPicture.png" />

Deze repository beschrijft de **embedded sensormodule** (sensor node) voor het
monitoren van omgevingscondities in spouwmuren binnen het overkoepelende
BatSense-project.  
De module is opgebouwd rond een **ESP32-S2 (S2 Mini)** met **ESPHome**, een
**SHT30/SHT3X** temperatuurs- en vochtigheidssensor en een
**PowerBoost 500 Charger** voor batterijvoeding.  
De meetdata wordt via **Wi‑Fi** verstuurd en gekoppeld aan het centrale
systeem zoals beschreven in de BatSenseEmbedded-repository.

---

## Context binnen het BatSense-project

Dit werk maakt deel uit van een breder onderzoeksproject rond vleermuizen en
spouwmuren, waarin verschillende deelteams samenwerken:

- Een **embedded team** (BatSenseEmbedded) dat de algemene architectuur,
  datastroom en centrale verwerking uitwerkt.
- Dit deelproject, dat focust op een **draagbare sensor node** op basis van
  ESPHome voor omgevingsmonitoring in spouwmuren.
- Andere deelteams die zich o.a. richten op detectie, data-analyse en
  visualisatie.

In de centrale BatSenseEmbedded-repo wordt de globale opbouw van het systeem,
de communicatie en de rol van de verschillende nodes beschreven.  
Deze repo zoomt in op de **ESPHome-gebaseerde node** die temperatuur- en
vochtigheidsdata levert aan dat grotere systeem.

---

## Doelstelling

De voornaamste doelstellingen van deze sensor node zijn:

- Een **compacte, draagbare hardwaremodule** ontwikkelen voor gebruik in
  spouwmuren.
- **Temperatuur** en **luchtvochtigheid** betrouwbaar meten met een SHT30/SHT3X.
- Alle sensoren via **ESPHome** aan de S2 Mini koppelen.
- De meetdata **via Wi‑Fi** beschikbaar maken voor het centrale BatSense-systeem
  (bijv. integratie in een datalogger, Home Assistant of een eigen backend).
- De hardware en firmware voldoende documenteren zodat de node
  **reproduceerbaar** is door andere teamleden.

Dit sluit aan bij de globale projectdoelen: beter begrijpen hoe vleermuizen
spouwmuren gebruiken en bouwkundige richtlijnen ontwikkelen die ecologisch
verantwoord zijn.

---

## Hardwareoverzicht

De sensor node bestaat uit de volgende hoofdcomponenten:

- **S2 Mini (ESP32-S2)**  
  Microcontroller met geïntegreerde Wi‑Fi, geschikt voor ESPHome.
- **PowerBoost 500 Charger**  
  Zorgt voor batterijvoeding en laadfunctionaliteit.
- **SHT30/SHT3X sensor**  
  Meet **temperatuur** en **relatieve luchtvochtigheid** in de spouwmuur.

Belangrijke aspecten die ook binnen het BatSenseEmbedded-project aandacht
krijgen, zijn:
- **Energiebeheer** (deep-sleep, duty cycle, batterijduur)
- **Robuustheid** (vocht, condensatie, plaatsing in spouwmuur)
- **Betrouwbare Wi‑Fi-communicatie** naar het centrale systeem

De bekabeling, sensorplaatsing en praktische opbouw zijn beschreven in
`Docs/Research.md` en de aanvullende documenten in `Docs/`.

---

## Firmware, ESPHome en Datastroom

De firmware voor deze node wordt volledig gerealiseerd met **ESPHome**:

- ESPHome wordt gebruikt om:
  - de **SHT3X-sensor** via I²C te declareren;
  - de **Wi‑Fi-configuratie** vast te leggen;
  - **deep-sleep** en meetintervallen in te stellen;
  - de meetdata als **entiteiten** beschikbaar te maken op het netwerk.

- Het centrale configuratiebestand:
  - `Scripts/HTSensor.yaml`

**Datastroom (lokaal):**
1. De ESP32-S2 wordt wakker uit deep-sleep.
2. ESPHome leest de SHT30/SHT3X uit (temperatuur, luchtvochtigheid).
3. De waarden worden via Wi‑Fi verstuurd en zijn beschikbaar voor:
   - een lokaal systeem (bijv. Home Assistant), of
   - een centrale component zoals gedefinieerd in BatSenseEmbedded
     (bijvoorbeeld een server die via MQTT/HTTP de data verzamelt).

Op die manier vormt deze node één van de **databronnen** binnen de
overkoepelende BatSense-architectuur.

---

## Projectstructuur

Docs/
Research.md
01_board_controle.md
02_sensor_kabels.md
03_s2mini_flashen.md
Attachments/
... (screenshots en foto’s van hardware en opbouw)

Scripts/
HTSensor.yaml


- `Docs/`  
  Bevat alle documentatie over de hardware, testprocedures en opbouwstappen.
- `Scripts/`  
  Bevat de ESPHome-configuratie (`HTSensor.yaml`) die de sensoren koppelt
  en de datadoorsturing via Wi‑Fi regelt.

Deze structuur sluit aan bij de manier waarop in BatSenseEmbedded de
verschillende onderdelen modulair zijn opgezet.

---

## Installatie en Gebruik

1. **Hardware opzetten**  
   Volg `Docs/Research.md` en de deelbestanden in `Docs/` voor:
   - aansluiting van S2 Mini, PowerBoost en SHT30/SHT3X;
   - controle van de voeding en signaallijnen;
   - eventuele aanpassingen aan sensorkabels en behuizing.

2. **ESPHome installeren en configureren**  
   - Installeer ESPHome op je ontwikkelmachine.
   - Plaats `HTSensor.yaml` in je ESPHome-projectmap.
   - Pas indien nodig Wi‑Fi-gegevens en sensorinstellingen aan.

3. **Firmware flashen**  

esphome run HTSensor.yaml

Dit compileert de configuratie en uploadt de firmware naar de S2 Mini.

4. **Testen en logs bekijken**  
esphome logs HTSensor.yaml

Gebruik deze logs om te controleren:
- of de SHT30/SHT3X correct wordt uitgelezen;
- of de Wi‑Fi-verbinding werkt;
- of de entiteiten zichtbaar zijn voor het centrale systeem
  (bijvoorbeeld volgens de afspraken uit BatSenseEmbedded).

---

## Resultaten en Rol binnen het Teamproject

Met deze sensor node kan in spouwmuren een stabiele meting van
**temperatuur** en **luchtvochtigheid** uitgevoerd worden.  
Binnen het bredere BatSenseEmbedded-project levert deze node:

- Relevante **omgevingsdata** rond de leefomgeving van vleermuizen.
- Een **praktisch voorbeeld** van een energiezuinige, draadloze IoT-node.
- Een **reproduceerbare hardware- en firmwarebasis** voor verdere uitbreiding
(bijvoorbeeld extra sensoren, andere locaties, meer nodes).

De ervaringen uit dit deelproject (energiebeheer, vochtproblemen,
connectiviteit) sluiten aan bij de algemene ontwerpbeslissingen in de
BatSenseEmbedded-architectuur.

---

## Conclusie

Deze repository documenteert de ESPHome-gebaseerde sensor node binnen het
BatSense-project.  
Door de combinatie van **S2 Mini**, **PowerBoost**, **SHT30/SHT3X** en
**ESPHome** ontstaat een robuuste, draagbare sensormodule die goed integreert
in de centrale BatSenseEmbedded-opzet.

De duidelijke scheiding tussen:
- hardware (Docs/),
- firmwareconfiguratie (Scripts/),
- en de centrale architectuur (BatSenseEmbedded-repo),

maakt het voor andere teamleden mogelijk de node te begrijpen, te
reproduceren en verder te integreren in het volledige systeem.
