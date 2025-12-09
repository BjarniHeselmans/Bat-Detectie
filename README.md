# Vleermuizen en Spouwmuren – ESPHome Sensor Node

<img width="2480" height="1642" alt="image" src="https://github.com/BjarniHeselmans/Bat-Detectie/blob/main/Docs/Attachments/ProjectPicture.png" />

## 1. Inleiding — Waarom bestaat dit project?

Dit project maakt deel uit van het BatSense-onderzoek rond vleermuizen en spouwmuren binnen de opleiding Elektronica-ICT aan Hogeschool PXL.  
Vleermuizen maken gebruik van spouwmuren als leef- en verplaatsingsruimte. Om dat gebruik beter te begrijpen, is betrouwbare monitoring van de omgevingscondities (zoals temperatuur en luchtvochtigheid) in die spouwmuren nodig.

Binnen het grotere BatSenseEmbedded-project werken meerdere deelteams samen aan een modulair systeem met verschillende nodes en een centrale verwerking.  
Deze repository focust op één specifieke node: een compacte, batterijgevoede sensormodule op basis van een ESP32-S2 (S2 Mini) en ESPHome, die via Wi‑Fi meetdata uit de spouwmuur doorstuurt naar het centrale systeem, gevormd door Home assistant.

---

## 2. Doelstelling — Wat moest er op het einde werken?

Het doel van dit deelproject is een werkende, reproduceerbare sensor node op te leveren die:

- temperatuur en relatieve luchtvochtigheid in een spouwmuur kan meten met een SHT30/SHT3X-sensor;
- autonoom op batterij kan functioneren, met deep-sleep om energie te besparen;
- via ESPHome elke sensor logisch aan de ESP32-S2 koppelt;
- de gemeten waarden via Wi‑Fi doorstuurt naar een centraal systeem (bv. Home Assistant of een backend uit BatSenseEmbedded);
- voldoende gedocumenteerd is (hardware + firmware) zodat een andere student de node opnieuw kan bouwen en integreren in het BatSense-systeem.
- De node moet aantoonbaar meetdata leveren die in het centrale systeem zichtbaar en logbaar is.

Binnen het systeem fungeert Home Assistant als centraal punt voor:

- een realtime overzichtsdashboard met de actuele status van alle devices, inclusief duidelijke indicatie van online en offline nodes;
- automatische en continue datalogging van temperatuur- en luchtvochtigheidsdata per module;
- grafische visualisatie met minstens 30 minuten historiek per module en één gezamenlijke temperatuur-/humidity-grafiek voor alle modules;
- beheer en visualisatie van minstens 20 autonome sensormodules;
- persistente opslag van alle meetdata, ook na herstart van Home Assistant;
- correcte herinitialisatie na herstart waarbij alle nodes en data opnieuw zichtbaar zijn;
- visualisatie van MLX90640-thermische data als 32×24 warmtebeeld met logging van minimum-, maximum- en gemiddelde temperatuur;
- export van node-lijsten en meetdata naar CSV/Excel;
- ondersteuning voor het nemen van dashboardscreenshots;
- mogelijkheid tot het maken en opslaan van configuratie-back-ups.

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

De bekabeling, pinout en fysieke opstelling worden beschreven in de documenten in **[Docs/](./Docs/)**:
- **[Research.md](./Docs/Research.md)** – hardwareopzet en keuzes
- **[board_controle.md](./Docs/Board_controle.md)** – basiscontroles van de S2 Mini
- **[sensor_kabels.md](./Docs/SensorKabels.md)** – sensorbekabeling en aanpassingen
- **[s2mini_flashen.md](./Docs/S2mini_flashen.md)** – stappen om de S2 Mini te flashen met ESPHome

De Home Assistant-opstelling bestaat uit:

- **Softwareplatform (Home Assistant):**  
  Home Assistant OS als centraal automatisatie- en dataplatform.
- **Microcontroller / Host-systeem:**  
  Raspberry Pi 4 (2 GB) met **microSD-kaart (klasse 1)**.
- **Netwerk / Access point:**  
  TP-Link TL-MR6400 draadloze N 4G-LTE-router voor internet- en netwerkconnectiviteit.
- **Bekabeling:**  
  Voedingskabels en ethernetkabel voor stroomvoorziening en netwerkverbinding.

De communicatieprotocollen en fysieke opstelling worden beschreven in de documenten in **[Docs/](./Docs/)**.


### 3.2 Firmware & Software (ESPHome & Home Assistant)

De volledige firmware op de sensornodes wordt opgebouwd met **ESPHome** en gekoppeld aan **Home Assistant** als centraal verwerkings- en visualisatieplatform.  
Belangrijkste elementen:

- **Configuratiebestand (ESPHome):**  
  [Scripts/base.yaml](./Scripts/base.yaml)
- **Sensorconfiguratie:**  
  Declaratie van de SHT3X-sensor via I²C, inclusief meetfrequentie.
- **Energiebeheer:**  
  Deep-sleep-configuratie om de node slechts periodiek te laten meten en verzenden.
- **Wi-Fi-configuratie:**  
  In `base.yaml` worden SSID en wachtwoord ingesteld zodat de node automatisch verbinding maakt met het netwerk.
- **Datadoorsturing:**  
  ESPHome publiceert de meetwaarden als netwerkentiteiten.
- **Home Assistant-integratie:**  
  Home Assistant detecteert de ESPHome-nodes automatisch, registreert alle sensoren als entiteiten, logt de meetwaarden continu en visualiseert deze via dashboards en grafieken.
- **Dataopslag & historiek:**  
  Meetdata blijft persistent bewaard in Home Assistant en blijft beschikbaar na een herstart.

### 3.3 Architectuur en datastroom

De datastroom voor deze node verloopt als volgt:

1. De node wordt gevoed door de batterij via de PowerBoost 500 Charger.
2. De ESP32-S2 wordt wakker uit deep-sleep.
3. ESPHome leest de SHT30/SHT3X-sensor uit via I²C (temperatuur en luchtvochtigheid).
4. De ESP32-S2 maakt verbinding met het Wi‑Fi-netwerk.
5. ESPHome stuurt de gemeten waarden via Wi‑Fi naar het centrale systeem (bv. Home Assistant of een server binnen BatSenseEmbedded).
6. Home Assistant ontvangt de data, slaat deze persistent op, en visualiseert de meetwaarden via dashboards en grafieken.
7. De data kan vanuit Home Assistant verder worden geëxporteerd (CSV/Excel).

Deze node is daarmee één van de sensoren in het grotere BatSenseEmbedded-ecosysteem, waar meerdere nodes en servers samenwerken.

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

/----> future work: home assistant toont aan:
- aantal werkende modules
- screenshots home assistant
- temp/ hum grafieken
- camerabeelden met timestamps
// --> moet ook:
- wat is er effectief getest uitleg + resultaten
- werkt het stabiel leg uit?
- wat werkt wanneer waarom werkt iets niet? leg uit.

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

- **[Docs/](./Docs/)** bevat alle documentatie rond hardware, tests en opbouw.
- **[Scripts/](./Scripts)** bevat de ESPHome-configuratie waarmee de sensoren gekoppeld en via Wi‑Fi doorgestuurd worden.
- **[firmware/](./firmware/)** bevat dummy sensor logica.
