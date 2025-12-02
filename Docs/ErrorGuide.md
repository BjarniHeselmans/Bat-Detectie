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

# Optioneel: protobuf handmatig installeren

Alleen nodig als je ESPHome buiten een virtuele omgeving installeert (niet aanbevolen):

```bash
pip install "protobuf<5,>=4.25.3"
pip install esphome
```

---

# Aanbevolen werkwijze

Gebruik **altijd** een virtuele omgeving voor ESPHome om dependency-conflicten te vermijden.

---

Veel succes! 
