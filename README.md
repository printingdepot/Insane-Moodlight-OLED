![Insane Moodlight V2](insane-moodlight-v2.png)
Insane Moodlight OLED V2.0
Dieses Projekt ist mein Custom-Stimmungslicht, basierend auf ESPHome. Es ist kein billiger LED-Streifen, sondern eine durchdachte Hardware-Lösung mit Fokus auf Signalqualität, Displayschutz und einer persönlichen Note.

Warum "Insane"?
Ich habe hier nicht nur ein paar LEDs zusammengesteckt. Die Hardware ist auf Stabilität ausgelegt, und die Software löst echte Probleme wie OLED-Einbrennen und Akku-Management.

Die Hardware (Sauber aufgebaut!)
Wer LEDs mit 5V betreibt, weiß, dass der 3.3V Pegel vom ESP oft zickt. Deshalb steckt hier ein ordentlicher Aufbau drin:

Signalqualität: SN74AHCT125N Levelshifter für saubere 5V Datenpegel + 100nF Keramik-Kondensator zur Entstörung.

Schutz: 62 Ohm Widerstände in den Datenleitungen verhindern Reflexionen.

Spannungsstabilität: Massive Pufferung gegen Flicker! 220µF am ESP (3.3V) und gleich drei 470µF Elkos für die 5V Schiene und die LED-Ausgänge.

Sicherheit: Glassicherung für den Brandfall und ein anständiger LiPo-Laderegler für die Lithium-Zelle (inkl. Halterung).

Interaktion: 3x 6x6x6 Mikroschalter für die manuelle Steuerung.

Sensorik: DHT-Sensor und Batterieüberwachung über A0 (mit 100k Widerstand).

Was die Software alles regelt
Burn-In Protection: OLEDs brennen ein, wenn man nichts tut. Mein Code verschiebt das gesamte Bild alle 2 Minuten (Pixel-Shift), damit die Anzeige Jahre hält.

Greeting-System: Per Knopfdruck oder Home Assistant startet eine Sequenz mit schlagendem Herz, Stern oder Smiley – inkl. zwei Textzeilen, die man live ändern kann.

Master-Toggle: Ein langer Druck auf Taster 1 oder ein Klick in HA speichert die aktuellen Farbwerte in Globals und schaltet alles aus. Beim Wiedereinschalten kommt exakt dein Licht-Setup zurück.

Visueller Akku-Alarm: Wenn die Spannung einbricht, warnt das Licht von selbst:

Unter 10% -> Passive LEDs blitzen alle 10 Sek. rot auf.

Unter 5% -> Intervall verkürzt sich auf 5 Sek. (Laden angesagt!).

Boot-Logic: Beim Starten wird ein Logo angezeigt, ohne die im Flash gespeicherten persönlichen Nachrichten zu überschreiben.

Setup
secrets.yaml anlegen (WLAN, Keys).

Per ESPHome flashen.


In Home Assistant über die neue "Master Toggle" Entität oder die Slider für Helligkeit und Effekte (Love Pulse, Sternenfunkeln) steuern.
