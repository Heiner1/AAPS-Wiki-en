# Beschreibung
> ACHTUNG: Diese Methode ist derzeit nur möglich, wenn die Entwicklerversion (dev-branch) von AndroidAPS installiert wird. Diese Version kann noch Fehler enthalten und verschiedene Probleme machen. Deshalb ist die beschriebene Methode noch experimentell!

In dieser Variante ist das Smartphone **Samsung Galaxy S7** das "Herzstück" und die Schaltzentrale der Loop. Es liest mit der originalen, aber von der Community leicht modifizierten Dexcom-App das kontinuierliche Glukosemesssystem "Dexcom G5" aus und steuert auf Basis dieser Daten über die App "AndroidAPS" (AAPS) die Insulinpumpe "DanaR" von SOOIL (per Handeingabe auf Vorschlag der App oder vollautomatisch nach Eingabe der Mahlzeit-KH). Weitere Geräte werden nicht benötigt.

Die **Alarme** für zu niedrige oder zu hohe Glukosewerte werden nicht über die sehr eingeschränkte Dexcom-App (bietet nur wenige vorgegebene Sounds), sondern über die App "xDrip+" im Smartphone ganz nach individuellem Bedarf eingestellt. So können je nach Tages- oder Nachtzeit unterschiedliche Alarmtöne oder Vibrationen eingerichtet werden. 

Falls gewünscht, können alle aktuellen Glukose- und Behandlungsdaten auf einer **"Sony Smartwatch 3"** (SWR50) am Handgelenk angezeigt werden. Über die Smartwatch kann dann auch z.B. diskret das Mahlzeiten-Bolus gesetzt werden.

Das System funktioniert **offline**, also ohne dass zum Betrieb eine Datenverbindung des Smartphones zum Internet erforderlich ist. 

Dennoch können die Daten bei bestehender Datenverbindung automatisch zu **Nightscout** "in die Cloud" hochgeladen werden, um umfangreiche Auswertungen für den Arztbesuch zu erhalten oder jederzeit die aktuellen Werte mit Familienmitgliedern zu teilen.

# Benötigte Komponenten
1. [Samsung Galaxy S7](http://www.samsung.com/de/smartphones/galaxy-s7/overview/)
> Bezugsquelle: Elektrofachhandel, Internetshops

> Alternativen: siehe Android-Smartphones in der [Dexcom Kompatibilitätsliste](https://www.dexcom.com/ous-compatibility-page) (Punkt "Dexcom G5 Mobile App", NICHT die unter "Dexcom Follower App" Genannten)
2. [DanaR](https://www.ime-dc.de/de/insulintherapie/insulinpumpen/dana-r)
> Bezugsquelle: In Deutschland auf Rezept oder privat über die Firma [IME-DC GmbH](http://www.ime-dc.de) 
3. [Dexcom G5](https://www.nintamed.eu/p/products/dexcomg5)
> Bezugsquelle: In Deutschland auf Rezept oder privat über die Firma [Nintamed](https://www.nintamed.eu/)
4. Optional: [Sony Smartwatch 3 (SWR50)](https://www.sonymobile.com/de/products/smart-products/smartwatch-3-swr50/)
> Bezugsquelle: Da die Uhr ein Auslaufmodell ist, muss man im Fachhandel oder im Internet ggf. etwas suchen. Falls sie zu einem akzeptablen Preis nur in grellen Neonfarben erhältlich ist, dann kann man sie trotzdem bestellen und das Band tauschen. Hierfür gibt es bei eBay unter dem Suchbegriff "SWR50 adapter" Adapter, in die die Uhr exakt reinpasst und an die man jedes beliebige Uhrenband (in der passenden Größe) machen kann.

# Optional: Nightscout online einrichten
[Nightscout.info](http://www.nightscout.info/) ist eine Website, über die die meisten Daten der eingerichteten Loop "in der Cloud" gesammelt werden können. Das ermöglicht umfangreiche Statistiken und Auswertungen, aber auch die Synchronisation der Werte mit weiteren Geräten oder das Teilen der Behandlungsdaten mit Familienmitgliedern, Freunden oder Ärzten.

1. Nightscout über Heroku installieren

Hierzu nach folgender Anleitung vorgehen: [http://www.nightscout.info/wiki/welcome/set-up-nightscout-using-heroku](http://www.nightscout.info/wiki/welcome/set-up-nightscout-using-heroku)

> Tipp: Alle Zugangsdaten auf einem Zettel oder in einer Textdatei notieren!
***
2. Heroku-Variablen einrichten

* Auf [https://herokuapp.com/](https://herokuapp.com/) einloggen
* App-Namen auswählen
* Settings > Schaltfläche "Reveal Config Vars" anklicken
* Variablen hinzufügen oder wie folgt ändern:<br>
   ENABLE = `careportal boluscalc food bwp cage sage iage iob cob basal ar2 rawbg pushover bgi pump openapsbasal loop`<br>
   DEVICESTATUS_ADVANCED = `on`<br>
   PUMP_FIELDS = `reservoir battery clock`
<br><br>
Ein Alarm bei niedrigem Pumpen-Batteriestand in % kann wie folgt aktiviert werden:<br>
PUMP_WARN_BATT_P = `51`<br>
PUMP_URGENT_BATT_P = `26`

***
3. Nightscout-Website Version checken

* https://DEINAPPNAME.herokuapp.com/
* Menü über die drei waagerechten Striche rechts oben am Bildschirm anklicken
* Am Ende des Menüs muss "Nightscout Version 0.10.2-..." stehen

> Tipp: Falls eine ältere Version angezeigt wird, z.B. "0.10.1-...", dann muss Nightscout aktualisiert werden. Dazu nach der Anleitung unter [http://www.nightscout.info/wiki/welcome/how-to-update-to-latest-cgm-remote-monitor-aka-cookie](http://www.nightscout.info/wiki/welcome/how-to-update-to-latest-cgm-remote-monitor-aka-cookie) vorgehen. Sollte sich trotz erfolgreichem Update die Versionsanzeige nicht aktualisieren, dann ist noch ein "Redeploy" von Hand erforderlich, siehe die Anleitung [unter http://www.nightscout.info/wiki/welcome/how-to-update-to-latest-cgm-remote-monitor-aka-cookie/update-my-fork-troubleshooting-part-2](http://www.nightscout.info/wiki/welcome/how-to-update-to-latest-cgm-remote-monitor-aka-cookie/update-my-fork-troubleshooting-part-2).

# Computer/Notebook vorbereiten
Um aus dem frei verfügbaren OpenSource-Quellcode von AAPS eine Android-App selbst erstellen zu können, wird 
Android Studio auf dem Computer oder Notebook (Windows, Mac, Linux) benötigt > Installieren wie unter
[https://developer.android.com/studio/install.html](https://developer.android.com/studio/install.html) beschrieben

# Smartphone einrichten

## Firmware des Samsung Galaxy S7 überprüfen
* Menü > Einstellungen > Telefoninfo > Softwareinfo: Hier sollte "Android-Version 7.0" stehen (diese Version ist erfolgreich getestet)
* Falls nicht: Menü > Einstellungen > Software-Update durchführen

## Installation von unbekannten Quellen erlauben
Menü > Einstellungen > Gerätesicherheit > Unbekannte Quellen > Schieber nach rechts (= aktiv)

## Bluetooth aktivieren
Menü > Einstellungen > Verbindungen > Bluetooth > Schieber nach rechts (= aktiv)

## Dexcom App (modifizierte Version) installieren
Die Original-App von Dexcom aus dem Google Play Store wird nicht funktionieren, weil sie die Werte nicht an andere Apps weitergibt. Darum ist eine von der Community leicht modifizierte Version erforderlich. Nur sie kann später mit AAPS kommunizieren. Unter [https://github.com/dexcomapp/dexcomapp?files=1](https://github.com/dexcomapp/dexcomapp?files=1) ist eine mmol/l-Version und eine mg/dl-Version der modifizierten Dexcom-App hinterlegt. 


Dazu folgende Schritte ausführen:

1. Falls die Original-Dexcom-App bereits installiert ist: Sensor stoppen, App deinstallieren über Menü > Einstellungen > Apps > Dexcom G5 Mobile > Deinstallieren
2. Modifizierte Dexcom-App von [https://github.com/dexcomapp/dexcomapp?files=1](https://github.com/dexcomapp/dexcomapp?files=1) herunterladen.
> ACHTUNG: Derzeit ist die als mg/dl bezeichnete Version TROTZDEM in mmol/l! Die Entwickler beheben diesen Fehler hoffentlich bald. Bis dahin hilft eine direkte Kontaktaufnahme zu Milos Kozak über die einschlägigen Facebook-Gruppen...
3. Modifizierte Dexcom-App auf dem Smartphone installieren (= die heruntergeladene *.apk-Datei auswählen)
4. Modifizierte Dexcom-App starten, den Sensor nach Anweisung aktivieren / kalibrieren und die Aufwärmphase abwarten
5. Wenn die ersten beiden Kalibrierungen erfolgreich waren und die modifizierte Dexcom-App den aktuellen Wert anzeigt, dann im Menü (= drei waagerechte Striche links oben in der App) auf "Warnungen" und folgende Konfiguration einstellen<br>
* Akut niedrig `55mg/dl` (kann nicht deaktiviert werden)
* Niedrig `AUS`
* Hoher `AUS`
* Anstiegsrate `AUS`
* Abfallrate `AUS`
* Signalverlust `AUS`
* Kurzer Blick `EIN` (kann auch deaktiviert werden, aber die Anzeige des aktuellen Glukosewerts in der Statuszeile des Smartphones ist praktisch)

## AAPS installieren
> Hinweis: Sobald die modifizierte Dexcom-Software in der Version 1.56 von AAPS enthalten ist, muss nicht mehr auf die Entwicklungsversion dev zurückgegriffen werden. Dieser Schritt muss dann im Wiki angepasst werden.

1. https://github.com/MilosKozak/AndroidAPS
2. Branch "dev" auswählen
3. Schaltfläche "Clone or download" > Download ZIP auswählen
4. Heruntergeladene ZIP-Datei in einem neuen Ordner entpacken
5. Android Studio starten
6. Der Anleitung unter [https://github.com/MilosKozak/AndroidAPS/wiki/APK-erstellen_de](https://github.com/MilosKozak/AndroidAPS/wiki/APK-erstellen_de) folgen
> Wichtig: Die Variante "fullWearControl-Release" verwenden!
7. Die erstellte *.apk-Datei auf das Smartphone laden / per E-Mail schicken und dort installieren
8. AAPS im Smartphone starten und folgende Einstellungen unter dem Menüpunkt **Config Builder** vornehmen:
* Profil: je nach Wunsch
* Insulin: das verwendete Insulin auswählen
* BZ Quelle: `Dexcom G5 App (patched)`, dann auf das Zahnrädchen, Upload BG data to NS `aktivieren` (falls Nightscout verwendet werden soll), Send BG data to xDrip+ `aktivieren`
* Pumpe: DanaR
* Empfindlichkeitserkennung: je nach Wunsch
* APS: je nach Wunsch
* Loop: aktivieren
* Beschränkungen: Zielsetzungen aktivieren
* Treatments: Behandlungen aktivieren
* Generell: Aktionen, Careportal, Laufende Benachrichtigungen jeweils aktivieren
* "Integrierter NSClient" aktivieren und im Zahnrädchen daneben: Nightscout URL = `https://DEINAPPNAME.herokuapp.com`, Nightscout API-Key = `DEINAPIKEY`, Aktiviere lokalen Broadcast = `aktivieren`, Alarm-Optionen = `alles deaktiviert`


## xDrip+ installieren
xDrip+ ist eine weitere ausgereifte App, die unzählige Möglichkeiten bietet. Anders als von den Entwicklern eigentlich gedacht, wird xDrip+ aber bei dieser Methode nicht auch zum Sammeln der Glukosedaten vom Dexcom G5 verwendet, sondern nur, um Alarme auszugeben und auf dem Android-Homescreen im Widget den aktuellen Gluosewert samt Kurve anzuzeigen. Mit xDrip+ können die Alarme nämlich viel individueller eingestellt werden als mit der Dexcom-Software, AAPS oder Nightscout (keine Einschränkung bei der Auswahl der Sounds, verschiedene Alarme je nach Tages-/Nachtzeit etc.).

1. Letzte stabile apk-Version von xDrip+ mit dem Smartphone herunterladen unter [https://xdrip-plus-updates.appspot.com/stable/xdrip-plus-latest.apk](https://xdrip-plus-updates.appspot.com/stable/xdrip-plus-latest.apk) - nicht die Version aus dem GooglePlay-Store!

2. xDrip+ installieren, indem die *.apk-Datei ausgewählt wird

3. xDrip+ starten und im Menü (drei waagerechte Striche links oben) folgende Einstellungen vornehmen:

* Einstellungen > Warnungen > Glukose-Alarm-Liste > Warnungen (niedrig) und (hoch) je nach Bedarf erstellen. Die bestehenden Alarme können mit einem langen Fingerdruck auf geändert werden
* Einstellungen > Kalibrierungs-Erinnerungen: deaktiviert (wird über die Dexcom-App erinnert)
* Einstellungen > Datenquelle > 640G/EverSense
* Einstellungen > Inter-App-Einstellungen > Accept Calibrations > AN
* Menü > Sensor starten (sonst kommt regelmäßig eine Fehlermeldung)

4. Auf dem Android Homescreen an eine freie Stelle lange drücken > Widgets > "xDrip+" auswählen, halten und an die gewünschte Stelle ziehen > loslassen

## Energiesparoptionen deaktivieren
Im Samsung Galaxy S7 auf Menü > Einstellungen > Gerätewartung > Akku > Nicht überwachte Apps > +Apps hinzufügen: Hier nacheinander die Apps AndroidAPS, Dexcom G5 Mobile, xDrip+ und ggf. AndroidWear auswählen (falls die Smartwatch verwendet wird)

## Optional: Sony Smartwatch 3 (SWR50) einrichten
Mit der Smartwatch lässt sich das Leben mit Diabetes noch viel unauffälliger gestalten. Über sie kann am Handgelenk jederzeit der aktuelle Glukosezucker, der Status der Loop etc. angezeigt werden und es können Bolusgaben vorgenommen werden. Dazu wie folgt vorgehen:

* In AAPS: Config Builder > Generell > Wear > aktivieren und im Zahnrädchen daneben: Steuerung von der Uhr - aktiv
* In der Smartwatch: Einstellungen > Ziffernblatt ändern > AAPSv2

# Pumpe einrichten
- Text folgt -
