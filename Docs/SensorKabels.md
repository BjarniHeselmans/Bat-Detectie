# Aanpassing en Controle van de Sensorbekabeling

## Overzicht
In dit deel van het project hebben we de **sensorbekabeling** van de **SHT3X-sensoren** aangepast en gecontroleerd.  
Tijdens de voorbereidende fase merkten we dat de bestaande kabels te lang waren om een betrouwbare I²C-communicatie te garanderen.  
Het doel van deze aanpassing was om de communicatiekwaliteit tussen de **S2 Mini** en de **SHT3X-sensoren** te verbeteren door de kabellengte te beperken tot een optimale lengte.

## Achtergrond
De **I²C-communicatiebus** (Inter-Integrated Circuit) is gevoelig voor signaalverzwakking en interferentie bij langere kabels.  
Na overleg met de onderzoeker hebben we besloten om de kabels tot ongeveer **1 meter** te knippen, afhankelijk van factoren zoals afscherming, omgeving en de kwaliteit van de verbindingen.  
De oorspronkelijke bekabeling overschreed deze lengte ruim, wat kon leiden tot:
- Onbetrouwbare of incomplete datatransmissie  
- Timingproblemen tussen de master (S2 Mini) en de slave (SHT3X)  
- Hogere kans op storingen door omgevingsruis  

## Werkwijze
1. **Overleg en bepaling van kabellengte**  
   In overleg met de onderzoeker werd besloten om de kabellengte te beperken tot **1 meter**.  
   Dit bood een goede balans tussen flexibiliteit in de opstelling en betrouwbaarheid van de I²C-communicatie.

2. **Inspectie van de bestaande kabels**  
   Voorafgaand aan het inkorten werden alle kabels grondig geïnspecteerd op:
   - Mechanische schade  
   - Corrosie of **waterschade** aan de connectoren en isolatie  
   - Eventuele loszittende verbindingen  

3. **Aanpassing van de lengte**  
   De kabels werden zorgvuldig **afgemeten, op 1 meter afgeknipt** en vervolgens **gestript** om de aders opnieuw te kunnen verbinden.

4. **Herverbinden van de sensor**  
   De **SHT3X-sensoren** werden opnieuw aangesloten volgens de **officiële datasheet**.  
   Hierbij werd gecontroleerd dat:
   - De **VIN**, **GND**, **SCL** en **SDA** pinnen correct waren verbonden.  
   - Er geen kortsluiting of omgekeerde polariteit kon ontstaan.  
   - De verbindingen stevig en schoon waren om betrouwbare datacommunicatie te verzekeren.

### Foto van de aangepaste sensorbekabeling
Onderstaande afbeelding toont een voorbeeld van een sensor met de aangepaste kabellengte en correcte aansluiting:

![SHT3X sensor met kabel](./Attachments/SensorCable.png)

## Observaties
- De kwaliteit van de verbindingen is visueel gecontroleerd en goedgekeurd.  

## Resultaat
- Alle sensoren zijn voorzien van **nieuwe, verkorte kabels** van 1 meter lengte.  
- De verbindingen zijn **volgens datasheet** gecontroleerd en bevestigd.  
