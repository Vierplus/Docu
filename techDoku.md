# Technische Dokumentation

## Schnittstellen und Implementierung

### Tailscale

- **Beschreibung**: Tailscale wird als VPN-Verbindung zwischen allen Geräten verwendet.
- **Implementierung**:
  - Tailscale auf allen Geräten installiert und konfiguriert.
  - Geräte in das gleiche Tailscale-Netzwerk integriert, um sichere Kommunikation zu gewährleisten.

### Raspberry Pi

- **Funktion**: Server für verschiedene Dienste.
- **Komponenten**:
  - **OPC UA Server**: Implementiert in Python zur Bereitstellung von Temperatur- und Feuchtigkeitsdaten.
  - **TCP IP Server**: Implementiert in Python zur Kommunikation mit der Kamera.
  - **Kamera**: Verwendet `cv2` für Bildverarbeitung und Extraktion von Hex-Werten.
- **Implementierung**: Python-Skripte zur Verwaltung von OPC UA und TCP IP Kommunikation.

### Virtuelle Maschine (VM)

- **Funktion**: Datenmanagement und Nachrichtenaustausch.
- **Komponenten**:
  - **MongoDB**: Datenbank zur Speicherung der Messdaten.
  - **Mosquitto**: MQTT Broker zur Nachrichtenvermittlung.
  - **Publisher Script**: Python-Skript, das Daten aus MongoDB liest und an den MQTT Broker sendet.
- **Implementierung**: MongoDB und Mosquitto auf der VM installiert und konfiguriert, Publisher Script zur Datenverarbeitung eingerichtet.

### Laptop 1

- **Funktion**: Datensammlung, Steuerung des Dobot Roboterarms und Datenübertragung.
- **Komponenten**:
  - **Dobot Roboterarm**: Wird gesteuert, um Würfel zu sortieren.
  - **OPC UA Client**: Abfrage von Temperatur- und Feuchtigkeitsdaten vom Raspberry Pi.
  - **TCP IP Client**: Abfrage der Hex-Werte der Kamera vom Raspberry Pi.
  - **Datenübertragung**: Sendet gesammelte Daten über Tailscale in die MongoDB der VM.
- **Implementierung**: Python-Skript zur Steuerung des Dobot Roboterarms und zur Kommunikation über OPC UA und TCP IP.

### Laptop 2

- **Funktion**: Datenvisualisierung.
- **Komponenten**:
  - **Angular Application**: Frontend-Anwendung zur Visualisierung der Daten.
  - **WebSocket**: Zugriff auf den MQTT Broker zur Echtzeit-Datenanzeige.
- **Implementierung**: Angular-Anwendung mit Angular Material, TypeScript und `ngx-charts` zur Visualisierung von Daten.

## Nutzung der Schnittstellen

### Tailscale

- **Installation**: Tailscale auf jedem Gerät installieren.
- **Konfiguration**: Geräte im gleichen Tailscale-Netzwerk hinzufügen.

### Dobot Roboterarm und Clients (Laptop 1)

- **Starten**: Python-Skript ausführen, das folgende Aufgaben erledigt:
  - **Würfel aufnehmen und zur Kamera bringen**: Der Roboterarm nimmt den Würfel auf und bringt ihn zur Kamera.
  - **Hex-Wert von Kamera erhalten**: Die Kamera gibt einen Hex-Wert aus.
  - **Hex-Wert umwandeln**: Der TCP IP Client empfängt den Hex-Wert und wandelt ihn in RGB um.
  - **Farbbestimmung**: Der RGB-Wert wird zur Bestimmung der Farbe verwendet.
  - **Temperatur- und Feuchtigkeitsdaten abfragen**: Der OPC UA Client gibt nebenher die Temperatur und Luftfeuchtigkeit aus.
  - **Würfel sortieren**: Der Roboterarm sortiert den Würfel in den entsprechenden Bereich basierend auf der Farbe.
  - **Datenübertragung**: Alle Daten werden über `pymongo` in die MongoDB geschrieben.

### Angular Application (Laptop 2)

- **Starten**: Angular-Anwendung ausführen, WebSocket zur Verbindung mit dem MQTT Broker verwenden.

## Datenbankstruktur (MongoDB)

### Aufbau

- **Datenbank**: `VM_DB`
- **Collection**: `Data_Collection`
- **Datenformat**: JSON

### Beispiel-Dokument

```json
{
  "measurement_no": 1,
  "measurement_timestamp": "2024-04-23 12:00:00",
  "component_no": 1,
  "component_color_hex": "#336699",
  "component_color_name": "Blau",
  "current_temp_c": 25.5,
  "current_humidity": 60,
  "current_power_consumption": 0.2,
  "current_price": 0.996
}
```

### Nutzung der Datenbank

- **Zugriff**: Über MongoDB Compass.
- **Anmeldung**: Benutzername und Passwort erforderlich.
  - **Benutzername**: `vierplus`
  - **Passwort**: `4plus`
