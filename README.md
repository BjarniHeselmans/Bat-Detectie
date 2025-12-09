# Onderzoeksproject: Vleermuizen en Spouwmuren

Dit project beschrijft een embedded sensormodule voor het monitoren van
vleermuisactiviteit en omgevingscondities in spouwmuren, opgebouwd rond een
ESP32-S2 (S2 Mini), een SHT30 temperatuurs- en vochtigheidssensor en een
batterijvoedingsmodule met draadloze datadoorsturing via ESPHome.

---

## Inleiding

Dit project kadert binnen de opleiding Elektronica-ICT aan Hogeschool PXL en
sluit aan bij een breder onderzoeksopzet rond monitoring, IoT en ecologie.  
De sensormodules worden ingezet om het gebruik van spouwmuren door vleermuizen
te bestuderen aan de hand van omgevingsmetingen en beweging, met als doel
zowel **ecologische inzichten** als **praktische richtlijnen** voor
bouwkundige toepassingen te verzamelen.

---

## Doelstelling

Het doel is om een compacte, draagbare hardwaremodule te ontwikkelen die
temperatuur en luchtvochtigheid in spouwmuren betrouwbaar meet en de gegevens
draadloos doorstuurt naar een overkoepelend systeem.

De module moet:
- autonoom op batterij kunnen werken;
- reproduceerbaar zijn op basis van de documentatie;
- via de ESPHome-configuratie aantoonbaar meetdata leveren die in een hoger
  niveau platform (zoals Home Assistant of een dataloggingomgeving) kan
  worden gebruikt.

---

## Materialen en Methoden

De hardware bestaat uit:
- S2 Mini (ESP32-S2 met Wi‑Fi);
- PowerBoost 500 Charger voor batterijvoeding en laadfunctie;
- SHT30/SHT3X sensor voor temperatuur- en vochtigheidsmeting.

De bekabeling en opstelling zijn beschreven in `Docs/Research.md`.

De firmware wordt gerealiseerd met **ESPHome** op basis van:
- `Scripts/HTSensor.yaml`

Hiermee:
- leest de ESP32-S2 de SHT3X via I²C uit;
- wordt deep-sleep gebruikt om batterij te sparen;
- worden gemeten waarden periodiek via Wi‑Fi verstuurd.

---

## Projectstructuur

Docs/
Research.md
01_board_controle.md
02_sensor_kabels.md
03_s2mini_flashen.md
Attachments/
... (screenshots en foto’s)

Scripts/
HTSensor.yaml


- `Docs/` bevat alle documentatie rond hardware, tests en opbouw.  
- `Scripts/` bevat de ESPHome-configuratiebestanden.

---

## Installatie en Gebruik

1. **Hardware opzetten**  
   Volg `Docs/Research.md` voor het aansluiten van:
   - S2 Mini  
   - PowerBoost  
   - SHT30/SHT3X sensor

2. **Firmware flashen**  
   Gebruik ESPHome met het YAML-bestand in `Scripts/`:
   esphome run HTSensor.yaml

3. **Testen en logs bekijken**  
   esphome logs HTSensor.yaml

Bekijk hiermee in realtime de sensorwaarden en controleer de communicatie.

---

## Resultaten

Met de opgeleverde module kan in spouwmuren een stabiele meting van temperatuur
en luchtvochtigheid uitgevoerd worden, waarbij de sensordata via ESPHome
beschikbaar komt als entiteiten die door een extern systeem gelogd en
gevisualiseerd kunnen worden.

De combinatie van documentatie in `Docs/` en configuratie in `Scripts/`
maakt het mogelijk om:
- de opstelling te reproduceren;
- het gedrag van de module te testen;
- de meetresultaten te koppelen aan het bredere vleermuisonderzoek.

---

## Conclusie

De combinatie van S2 Mini, PowerBoost en SHT30 levert een praktische embedded
oplossing voor omgevingsmonitoring in spouwmuren, met een duidelijke scheiding
tussen hardwaredocumentatie en firmwareconfiguratie in de repository.

Tijdens het project komen typische embedded-uitdagingen zoals energiebeheer,
omgevingsinvloeden (vocht) en draadloze connectiviteit expliciet in beeld.
Dit biedt waardevolle leerervaringen voor het ontwerpen van robuuste
IoT-sensorknopen in realistische toepassingen.
