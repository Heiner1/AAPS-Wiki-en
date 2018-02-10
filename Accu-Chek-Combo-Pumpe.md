WORK IN PROGRESS

Die Software ist Teil einer DIY-Lösung(Do It Yourself = Eigenbau) und kein Produkt. Daher bist **Du **gefordert. **Du **musst lesen, lernen und verstehen was das System macht und wie du es bedienst.
Das System wird Dir nicht alle Schwierigkeiten Deiner Diabetestherapie abnehmen, aber wenn Du Willens bist die nötige Zeit zu investieren, dann kann es die Ergebnisse Deiner Therapie verbessern und die Lebensqualität erhöhen. Dir sollte klar sein, dass das System umso besser arbeitet je besser Deine Therapiegrundeinstellung ist.
Hetz Dich nicht auch wenn andere Dir erzählen wie toll das alles ist. Nimm Dir Zeit zu lernen!
Du bist ganz alleine dafür verantwortlich was Du mit dem System machst.


Hardware requirements

    Eine Roche Accu-Chek Combo Pumpe (egal welche Firmware, es funktionieren alle)

    Einen Smartpix oder Realtyme Adapter und die Accu-Chek 360 Konfigurationssoftware um die Pumpe zu konfigurieren. Kunden von Roche können die Software beim Kundendienst erfragen.

   Ein kompatibles Telefon: Ein Android Telefone mit LineageOS 14.1 (früher CyanogenMod) oder Android 8.1 (Oreo). Eine Liste gestester Telefone findet sich hier https://docs.google.com/spreadsheets/d/1-Im_rTkWPbk-Pl_hlnh-GhfZbAlXbh4PiLNnBJqGFyk/edit#gid=0. Die Liste ist nicht abschliessend und spiegelt nur die persönliche Erfahrung der Benutzer wieder. Bitte trage Deine Erfahrung in die Liste ein und hilf damit anderen. Die ganzen DIY Projekte funktionieren nur, wenn jeder etwas zurückgibt. 

    Vorsicht, obwohl man unter Android 8.1 mit der Combo Pumpe kommunizieren kann, gibt es noch Schwierigkeiten mit AAPS unter Android 8.1. Für Fortgeschrittene erfahrene Anwender gibt es noch die Möglichkeit Bluetooth Pairing zwischen Pumpe und einem gerooteten Android Telefon (Android 4.2) vorzunehmen und die Informationen dann auf ein anderes gerootetes Handy (Android > 5 ) zu übertragen, damit ruffy/AAPS auf dem zweiten Handy läuft.
Dieses Vorgehen erlaubt die Verwendung eines Android < 8.1 es ist aber nicht großartig getestet und auch kein sehr verbreitetes Verfahren. https://github.com/gregorybel/combo-pairing/blob/master/README.md
Wenn Dir rooten/pairen und so weiter nichts sagen, dann ist die letzte Variante vermutlich nichts für Dich.

Beschränkungen

    Verzögerter Bolus und Multiwave-Bolus werden nicht unterstützt.
    Es wird nur ein Basalprofil unterstützt.
    Das setzen mehrerer Basalprofile oder die Abgabe eines verzögerten Bolus oder eines Multiwave-Bolus stört das Konzept von temporären Basalraten und setzt den Loop für 6h in einen low glucose suspend mode, da unter diesen Umständen keine sichere Funktion des Closed Loops gewährleistet ist.
   Derzeit kann man Zeit und Datum auf der Pumpe nicht über das Telefon einstellen, Sommer/Winterzeit Umstellungen oder Umstellungen andere Zeitzonen müssen daher händisch vorgenommen werden (automatisches einstellen der Uhr des Telefons am Vorabend abstellen erst wieder einstellen, wenn die Uhrzeit auf der Pumpe angepasst wurde).

   Basalraten werden nur im Bereich von 0,05 bis 10 U/h unterstützt ( das gilt auch, wenn die Basalrate temporär geändert wird, beispielsweise kann eine Basalrate von 5 U/h auf maximal 200% gesetzt werden und eine Basalrate von 0,1 U/h nicht weiter als auf 50% reduziert werden)._**stimmt das so?**_
Wenn der Loop eine laufende Basalrate abbrechen will, wird stattdessen die Basalrate für 15 min. auf 90% oder 110% gesetzt. Das ist nötig, weil das Abbrechen der Basalrate auf der Combo Pumpe einen Alarm (W6 TBR Abbruch) auslöst, der durch starke Vibrationen mittgeteilt wird.
Manchmal kann es vorkommen, dass AAPS einen W6 TBR Abbruch Alarm nicht selbst quittiert, dann muss der Benutzer die Warnung selbst bestätigen entweder durch bestätigen des Alarms auf der Pumpe oder durch den Refresh Button im Combo Tab die Warnung an AAPS übergeben, damit AAPS die Warnung bestätigen kann.

Die Stabiltät der Bluetooth Verbindung variiert je nach verwendetem Telefon stark, dies kann zu "pump unreachable" Alarmen führen, und verhindern, dass die Verbindung zur Pumpe hergestellt werden kann. Wenn dieses Verhalten auftritt, prüfe ob
a) BT auf dem Telefon eingeschaltet ist
b) Refresh im Combo Tab von AAPS die Verbindung wieder herstellt.

Versuche das Telefon neu starten, wenn die Schritte a und b nicht erfolgreich waren.
Wenn alles oben genannte nicht hilft, dann kann es nötig sein auf der Pumpe einen Knopf zu drücken (dadurch wird BT auf der Pumpe gestoppt und neu gestartet).
Derzeit ist nicht absehbar, dass dieses Verhalten verhindert werden kann. Wenn diese Fehler öfter auftreten, dann besteht die derzeit einzige Lösung in der Verwendung eines Telefons, von dem bekannt ist, dass es zuverlässig mit der Combo unter AAPS zusammenarbeitet (unten gibt es eine kurze Liste von Telefonen).

Bolusabgabe direkt an der Pumpe wird von AAPS erkannt (immer wenn AAPS sich mit der Pumpe verbindet), im ungünstigsten Fall, kann das aber bis zu 20 minuten dauern. Bevor mittels AAPS die Basalrate über 100% erhöht wird oder ein Bolus abgegeben wird überprüft AAPS ob ein Bolus an der Pumpe abgegeben wird. Es wird dennoch empfohlen AAPS für alle Interaktionen mit der Pumpe zu verwenden.

Das Setzen einer TBR direkt auf der Pumpe ist im closed Loop Betrieb nicht nötig und sollte im Allgemeinen nicht vorgenommen werden. Das Erkennen einer manuell gesetzten Basalrate kann bis zu 20 min Dauern und wird bei der Berechung auch nur ab dem Zeitpunkt verwendet, zu dem die TBR von AAPS eingelesen wird. Das führt dazu, dass die im Körper befindliche Insulinmenge (IOB) falsch berechnet wird.