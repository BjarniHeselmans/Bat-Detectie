# ESPHome Installatiegids (zonder dependency-conflicten)

Deze handleiding legt uit hoe je ESPHome correct installeert in een aparte virtuele Python-omgeving zodat er geen conflicten ontstaan met andere pakketten zoals *mediapipe*.

---

## Waarom een virtuele omgeving?
Sommige pakketten vereisen **protobuf 4.x**, terwijl ESPHome **protobuf 5+** nodig heeft. Dit botst in één Python-installatie.  
Een virtuele omgeving voorkomt deze problemen.

---

# ESPHome installeren in een virtuele omgeving

## 1. Virtuele omgeving aanmaken
Maak een aparte map met een eigen Python-omgeving:

```bash
python -m venv esphome-env
```

---

## 2. Virtuele omgeving activeren

### **Windows**
```bash
esphome-env\Scripts\activate
```

Wanneer actief verschijnt `(esphome-env)` vóór je command prompt.

---

## 3. ESPHome installeren
Installeer ESPHome binnen deze omgeving:

```bash
pip install esphome
```

ESPHome kiest automatisch een geschikte protobuf-versie (5.x of 6.x).

---

# Projectstructuur

Plaats je ESPHome-configuratie (YAML-bestanden) in een normale gebruikersmap, bijvoorbeeld:

```
C:\Users\JouwNaam\Documents\ESPHome\
```

Ga daarna naar die map:

```bash
cd C:\Users\JouwNaam\Documents\ESPHome
```

---

# ESPHome gebruiken

## Firmware compileren en uploaden

```bash
esphome run device1.yaml
```

## Live logs bekijken

```bash
esphome log device1.yaml
```

---

# Verrificatie dat de sensor is geupload:
<img width="1025" height="683" alt="image" src="https://github.com/user-attachments/assets/967ced35-c57a-4679-ace3-532e041e8309" />
<img width="982" height="671" alt="image" src="https://github.com/user-attachments/assets/85cf47c3-bac5-41bf-bf7d-52182e4dbd2e" />

---

# Aanbevolen werkwijze

Gebruik **altijd** een virtuele omgeving voor ESPHome om dependency-conflicten te vermijden.

---

Veel succes! 
