# Handbuch zur Nutzung des Systems

## 1. Raspberry Pi (Tastatur Variante) aufbauen

1. **Hardware anschließen**

   - Stecken Sie die Micro SD Karte in den Raspberry Pi.
   - Verbinden Sie die Platine mit dem Bandkabel an den GPIO-Steckplatz.
   - Schließen Sie die Kamera an einen USB 2.0-Anschluss an.
   - Verbinden Sie die Maus mit einem anderen USB-Slot.
   - Schließen Sie das Micro HDMI-Kabel an den Raspberry Pi an und verbinden Sie es mit einem Monitor über den Adapter.
   - Stecken Sie das Stromkabel ein und lassen Sie den Raspberry Pi hochfahren.

2. **Software starten**
   - Öffnen Sie das Terminal über die Menüleiste.
   - Geben Sie folgenden Befehl ein und drücken Sie Enter:
     ```bash
     python /MESSESTAND/__main__.py
     ```
   - Warten Sie, bis das Programm Rückmeldung gibt und Temperatur sowie Luftfeuchtigkeit ausgibt.

## 2. Laptop 2 - DataVisualisation

1. **Angular Application starten**
   - Öffnen Sie die Angular Application in Visual Studio Code (VSC).
   - Öffnen Sie das interne Terminal und navigieren Sie in das Verzeichnis der Anwendung:
     ```bash
     cd data-visualisation
     ```
   - Starten Sie die Anwendung mit:
     ```bash
     ng serve --open
     ```
   - Warten Sie, bis sich der Browser öffnet und die Web-Anwendung anzeigt.

## 3. Laptop 1 und Dobot

1. **Dobot und Laptop verbinden**

   - Schließen Sie das Stromkabel an den Dobot an.
   - Verbinden Sie den Dobot und Laptop 1 mit einem USB-Kabel.
   - Öffnen Sie das Terminal (CMD) und führen Sie folgenden Befehl aus:
     ```bash
     python3 /path/main.py
     ```
   - Warten Sie, bis der Dobot sich bewegt und einen Piepton von sich gibt.

2. **Fehlerbehebung**

   - Sollte kein Piepton zu hören sein, geben Sie im Terminal `q` für disconnect ein und starten Sie das Programm erneut mit:
     ```bash
     python3 /path/main.py
     ```
   - Der Dobot sollte sich neu ausrichten und nach einiger Zeit einen Piepton ausgeben.

3. **Kamera positionieren**

   - Wählen Sie im Terminal `camera position` und folgen Sie den Anweisungen, um die Kamera richtig zu platzieren.
   - Drücken Sie Enter, damit der Dobot zur Ausgangsposition zurückkehrt.

4. **Würfel sortieren**
   - Platzieren Sie die Würfel auf den Positionen Q13, Q15, Q17 und Q19.
   - Wählen Sie `automatic mode` oder `manual mode` im Terminal:
     - **manual mode**: Wählen Sie selbst die Positionen aus und sortieren Sie die Würfel in eigener Reihenfolge.
     - **automatic mode**: Die Würfel werden automatisch von Q13 nach Q19 sortiert.
   - Lassen Sie den Dobot die Würfel sortieren.
   - Beenden Sie das Programm mit `disconnect` und schließen Sie das Terminal.

## Datenanzeige in der Web-Anwendung

Nach dem erfolgreichen Sortieren der Würfel werden die Daten in der Web-Anwendung als Charts und Statistiken angezeigt. Über das Dropdown-Menü können Sie eine Komponentennummer auswählen und die entsprechenden Werte vom Durchgang anzeigen lassen.

## Fehlerbehebung

- **Dobot Kalibrierung**: Sollte der Dobot nicht mittig über den Würfeln ausgerichtet sein, disconnecten Sie das Programm und starten Sie es neu, um die Kalibrierung durchzuführen.
- **Farberkennung**: Sollte der gelbe Würfel als grün angezeigt werden, platzieren Sie eine zusätzliche Lichtquelle neben die Kamera.
