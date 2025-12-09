# Vleermuizen en Spouwmuren – ESPHome Sensor Node

<img width="2480" height="1642" alt="image" src="https://github.com/BjarniHeselmans/Bat-Detectie/blob/main/Docs/Attachments/ProjectPicture.png" />

## 1. Inleiding — Waarom bestaat dit project?

Dit project maakt deel uit van het BatSense-onderzoek rond vleermuizen en spouwmuren binnen de opleiding Elektronica-ICT aan Hogeschool PXL.  
Vleermuizen maken gebruik van spouwmuren als leef- en verplaatsingsruimte. Om dat gebruik beter te begrijpen, is betrouwbare monitoring van de omgevingscondities (zoals temperatuur en luchtvochtigheid) in die spouwmuren nodig.

Binnen het grotere BatSenseEmbedded-project werken meerdere deelteams samen aan een modulair systeem met verschillende nodes en een centrale verwerking.  
Deze repository focust op één specifieke node: een compacte, batterijgevoede sensormodule op basis van een ESP32-S2 (S2 Mini) en ESPHome, die via Wi‑Fi meetdata uit de spouwmuur doorstuurt naar het centrale systeem.

---

## 2. Doelstelling — Wat moest er op het einde werken?

Het doel van dit deelproject is een werkende, reproduceerbare sensor node op te leveren die:

- temperatuur en relatieve luchtvochtigheid in een spouwmuur kan meten met een SHT30/SHT3X-sensor;
- autonoom op batterij kan functioneren, met deep-sleep om energie te besparen;
- via ESPHome elke sensor logisch aan de ESP32-S2 koppelt;
- de gemeten waarden via Wi‑Fi doorstuurt naar een centraal systeem (bv. Home Assistant of een backend uit BatSenseEmbedded);
- voldoende gedocumenteerd is (hardware + firmware) zodat een andere student de node opnieuw kan bouwen en integreren in het BatSense-systeem.

De node moet aantoonbaar meetdata leveren die in het centrale systeem zichtbaar en logbaar is.

---

## 3. Materialen & Methoden — Hoe is het gebouwd?

### 3.1 Hardware

De sensor node bestaat uit:

- **Microcontroller:**  
  ESP32-S2 Mini (S2 Mini) met geïntegreerde Wi‑Fi.
- **Sensor:**  
  SHT30/SHT3X voor temperatuur- en relatieve luchtvochtigheid (I²C-communicatie).
- **Voeding:**  
  PowerBoost 500 Charger voor batterijvoeding en laadfunctionaliteit.
- **Overige:**  
  Bekabeling, connectoren en een behuizing/opstelling geschikt voor plaatsing in een spouwmuur.

De bekabeling, pinout en fysieke opstelling worden beschreven in de documenten in `Docs/`:
- `Research.md` – hardwareopzet en keuzes
- `01_board_controle.md` – basiscontroles van de S2 Mini
- `02_sensor_kabels.md` – sensorbekabeling en aanpassingen
- `03_s2mini_flashen.md` – stappen om de S2 Mini te flashen met ESPHome

### 3.2 Firmware & Software (ESPHome)

De volledige firmware wordt opgebouwd met **ESPHome**.  
Belangrijkste elementen:

- **Configuratiebestand:**  
  `Scripts/HTSensor.yaml`
- **Sensorconfiguratie:**  
  Declaratie van de SHT3X-sensor via I²C, inclusief meetfrequentie.
- **Energiebeheer:**  
  Deep-sleep-configuratie om de node slechts periodiek te laten meten en verzenden.
- **Wi‑Fi:**  
  In `HTSensor.yaml` worden SSID en wachtwoord ingesteld zodat de node verbinding maakt met het gewenste netwerk.
- **Datadoorsturing:**  
  ESPHome maakt de sensorwaarden als entiteiten beschikbaar op het netwerk.  
  Deze kunnen door een centrale component (bv. Home Assistant of een server gedefinieerd in BatSenseEmbedded) worden ingelezen en gelogd.

### 3.3 Architectuur en datastroom

De datastroom voor deze node verloopt als volgt:

1. De node wordt gevoed door de batterij via de PowerBoost 500 Charger.
2. De ESP32-S2 wordt wakker uit deep-sleep.
3. ESPHome leest de SHT30/SHT3X-sensor uit via I²C (temperatuur en luchtvochtigheid).
4. De ESP32-S2 maakt verbinding met het Wi‑Fi-netwerk.
5. ESPHome stuurt de gemeten waarden via Wi‑Fi naar het centrale systeem (bv. Home Assistant of een server binnen BatSenseEmbedded).
6. Het centrale systeem logt en visualiseert de data, zodat deze kan worden gekoppeld aan het bredere vleermuisonderzoek.

Deze node is daarmee één van de sensoren in het grotere BatSenseEmbedded-ecosysteem, waar meerdere nodes en servers samenkomen.

---

## 4. Resultaten — Wat werkt effectief?

De volgende resultaten werden bereikt met deze sensor node:

- **Werkende hardwaremodule:**  
  De combinatie van S2 Mini, PowerBoost 500 Charger en SHT30/SHT3X levert een stabiel systeem op dat in een spouwmuur kan geplaatst worden.
- **Stabiele omgevingsmetingen:**  
  Temperatuur- en vochtigheidswaarden worden betrouwbaar uitgelezen via ESPHome.
- **Wi‑Fi-communicatie:**  
  De node maakt verbinding met het geconfigureerde Wi‑Fi-netwerk en publiceert de sensorwaarden als entiteiten.
- **Integratie met centraal systeem:**  
  De data kan worden ingelezen en gelogd door een hoger niveau platform (bijvoorbeeld Home Assistant of een centrale server binnen BatSenseEmbedded).

Het aantal werkende modules, testduur en stabiliteitstesten hangen af van de concrete metingen en opstellingen die in de loop van het project zijn uitgevoerd. Deze kunnen aangevuld worden met grafieken, logs en screenshots in de documentatie en in de centrale projectrapportage.

---

## 5. Besluit — Wat hebben we geleerd?

Uit dit deelproject rond de ESPHome sensor node kwamen de volgende inzichten naar voren:

- **Energiebeheer is cruciaal:**  
  Deep-sleep en meetinterval hebben een grote impact op de batterijduur. Het juist instellen hiervan is essentieel voor langdurige metingen in spouwmuren.
- **Omgevingsinvloeden:**  
  Vocht en condensatie vormen een risico voor de hardware. Het ontwerp van de behuizing en de plaatsing van de sensor zijn belangrijk voor de betrouwbaarheid.
- **Wi‑Fi-bereik en stabiliteit:**  
  In of rond een spouwmuur is het Wi‑Fi-signaal niet altijd optimaal. Dit moet meegenomen worden in de plaatsing van nodes en de keuze van access points.
- **Modulariteit binnen BatSenseEmbedded:**  
  Door ESPHome te gebruiken en de node duidelijk te documenteren, kan deze sensor eenvoudig geïntegreerd worden in de centrale BatSenseEmbedded-architectuur en door andere studenten worden nagebouwd of uitgebreid.

Deze node levert zo een concrete, technische bouwsteen voor het bredere vleermuis- en spouwmurenonderzoek, en illustreert hoe een robuuste, batterijgevoede IoT-sensorknoop ontworpen en gedocumenteerd kan worden.

---

## Projectstructuur (overzicht)

Docs/
Research.md
01_board_controle.md
02_sensor_kabels.md
03_s2mini_flashen.md
Attachments/
... (screenshots en foto’s)

Scripts/
HTSensor.yaml

text

- `Docs/` bevat alle documentatie rond hardware, tests en opbouw.
- `Scripts/` bevat de ESPHome-configuratie waarmee de sensoren gekoppeld en via Wi‑Fi doorgestuurd worden.
