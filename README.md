# Onderzoeksproject: Vleermuizen en Spouwmuren
<img width="2480" height="1642" alt="image" src="https://github.com/user-attachments/assets/67e67353-f503-4871-95e1-b014d2f404eb" />

## Introductie
Dit project onderzoekt hoe vleermuizen spouwmuren gebruiken als leef- en verplaatsingsruimte.  
We ontwikkelen sensormodules die temperatuur, luchtvochtigheid en beweging kunnen registreren.  
Het doel is om zowel **ecologische inzichten** te verkrijgen voor de bescherming van vleermuissoorten als **bouwkundige richtlijnen** te ontwikkelen voor renovatie en isolatie.

---

## Doel van het onderzoek
- In kaart brengen hoe vleermuizen spouwmuren benutten.  
- Begrijpen welke bouwkundige factoren (breedte, hoogte, openingen) hun beweging beïnvloeden.  

---

## Belang van het onderzoek
- **Ecologisch:** Bescherming van vleermuissoorten door beter inzicht in hun gedrag.  
- **Bouwkundig:** Bieden van richtlijnen om diervriendelijke renovatie en isolatie te ondersteunen.  

---

## Aanpak
Het onderzoek wordt uitgevoerd met behulp van:  
- Observaties met warmtecamera’s.  
- Akoestische detectie.  
- Ontwikkeling van compacte, draagbare sensormodules.  

---

## Terugblik vorig jaar
In een eerdere projectfase zijn de eerste sensormodules gebouwd.  
Daarbij kwamen enkele uitdagingen naar voren:  
- Beperkte batterijduur.  
- Problemen door vocht en condensatie.  
- Beperkingen in draadloze communicatie.  

---

## Hardwareoplossing
Om deze problemen aan te pakken, werken we met een nieuwe combinatie van componenten:  
- **[S2 Mini](https://github.com/BjarniHeselmans/Bat-Detectie/blob/main/Docs/Attachments/esp32-s2-mini.jpg)** (ESP32-S2 microcontroller met Wi-Fi).  
- **[PowerBoost 500 Charger](https://github.com/BjarniHeselmans/Bat-Detectie/blob/main/Docs/Attachments/Power-Boost-5000.jpg)** (voor batterijvoeding en opladen).  
- **[SHT30 sensor](https://github.com/BjarniHeselmans/Bat-Detectie/blob/main/Docs/Attachments/SHT30.jpg)** (voor temperatuur- en luchtvochtigheidsmetingen).
- [Deze set-up](https://github.com/BjarniHeselmans/Bat-Detectie/blob/main/Docs/Research.md)
 maakt het mogelijk om betrouwbare metingen te doen in spouwmuren en data draadloos door te sturen.  

---

## Doelstellingen
### Must-haves
- Ontwikkelen en opleveren van de hardwaremodule.  
- Documenteren in een Application Note.  
- Documenteren in deze GitHub README (Markdown).  
- Code review en versiebeheer via GitHub.  

### Nice-to-have
- Ontwerp en productie van een PCB.  

---

## Toepassingen
- Onderzoek naar vleermuizen in spouwmuren.  
- Algemeen draagbare IoT-projecten.  
- Sensoren en datalogging.  
- Omgevingsmonitoring (temperatuur en luchtvochtigheid).  

---

## Documentatie
- **Application Note:** Wordt toegevoegd in `/docs`.  
- **GitHub README:** [Dit document](https://github.com/BjarniHeselmans/Bat-Detectie/blob/main/README.md) met projectdoelen en hardwareoverzicht.  
- **Code:** Wordt toegevoegd in [/Src](https://github.com/BjarniHeselmans/Bat-Detectie/blob/main/Src/ESPCode.c).  

---

## Licentie
Dit project wordt uitgebracht onder de [MIT-licentie](LICENSE).  
