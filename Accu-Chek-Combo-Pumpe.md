# WORK IN PROGRESS

Die Software ist Teil einer DIY-Lösung(Do It Yourself = Eigenbau) und kein Produkt. Daher bist **DU** gefordert. **DU** musst lesen, lernen und verstehen was das System macht und wie du es bedienst.
Das System wird Dir nicht alle Schwierigkeiten Deiner Diabetestherapie abnehmen, aber wenn Du Willens bist die nötige Zeit zu investieren, dann kann es die Ergebnisse Deiner Therapie verbessern und die Lebensqualität erhöhen. Dir sollte klar sein, dass das System umso besser arbeitet je besser Deine Therapiegrundeinstellung ist.
Hetz Dich nicht auch wenn andere Dir erzählen wie toll das alles ist. Nimm Dir Zeit zu lernen!
Du bist ganz alleine dafür verantwortlich was Du mit dem System machst.


## Benötigte Hardware

* Eine Roche Accu-Chek Combo Pumpe (egal welche Firmware, es funktionieren alle)
* Einen Smartpix oder Realtyme Adapter und die Accu-Chek 360 Konfigurationssoftware um die Pumpe zu konfigurieren. Kunden von Roche können die Software beim Kundendienst erfragen.
* Ein kompatibles Telefon: Ein Android Telefone mit LineageOS 14.1 (früher CyanogenMod) oder Android 8.1 (Oreo). Eine Liste gestester Telefone findet sich hier https://docs.google.com/spreadsheets/d/1-Im_rTkWPbk-Pl_hlnh-GhfZbAlXbh4PiLNnBJqGFyk/edit#gid=0. Die Liste ist nicht abschliessend und spiegelt nur die persönliche Erfahrung der Benutzer wieder. Bitte trage Deine Erfahrung in die Liste ein und hilf damit anderen. Die ganzen DIY Projekte funktionieren nur, wenn jeder etwas zurückgibt. 
* Vorsicht, obwohl man unter Android 8.1 mit der Combo Pumpe kommunizieren kann, gibt es noch Schwierigkeiten mit AAPS unter Android 8.1. Für Fortgeschrittene erfahrene Anwender gibt es noch die Möglichkeit Bluetooth Pairing zwischen Pumpe und einem gerooteten Android Telefon (Android 4.2) vorzunehmen und die Informationen dann auf ein anderes gerootetes Handy (Android > 5 ) zu übertragen, damit ruffy/AAPS auf dem zweiten Handy läuft.
Dieses Vorgehen erlaubt die Verwendung eines Android < 8.1 es ist aber nicht großartig getestet und auch kein sehr verbreitetes Verfahren. https://github.com/gregorybel/combo-pairing/blob/master/README.md
Wenn Dir rooten/pairen und so weiter nichts sagen, dann ist die letzte Variante vermutlich nichts für Dich.

## Beschränkungen

* Verzögerter Bolus und Multiwave-Bolus werden nicht unterstützt.
* Es wird nur ein Basalprofil unterstützt.
* Das setzen mehrerer Basalprofile oder die Abgabe eines verzögerten Bolus oder eines Multiwave-Bolus stört das Konzept von temporären Basalraten und setzt den Loop für 6h in einen low glucose suspend mode, da unter diesen Umständen keine sichere Funktion des Closed Loops gewährleistet ist.
* Derzeit kann man Zeit und Datum auf der Pumpe nicht über das Telefon einstellen, Sommer/Winterzeit Umstellungen oder Umstellungen andere Zeitzonen müssen daher händisch vorgenommen werden (automatisches einstellen der Uhr des Telefons am Vorabend abstellen erst wieder einstellen, wenn die Uhrzeit auf der Pumpe angepasst wurde).
* Basalraten werden nur im Bereich von 0,05 bis 10 E/h unterstützt. Dies gilt auch für Anpassungen des Profiles, welches es erlaubt die Basalrate zu verdoppeln oder zu halbieren. Auch in diesem Fall müssen die Grenzwerte eingehalten werden, so dass die Basalrate maximal 5 E/h sein darf (da nach Verdoppelung 10 E/h), bzw. minimal 0,1 E/h (da nach Halbierung 0,05 E/h).
* Wenn der Loop eine laufende Basalrate abbrechen will, wird stattdessen die Basalrate für 15 min. auf 90% oder 110% gesetzt. Das ist nötig, weil das Abbrechen der Basalrate auf der Combo Pumpe einen Alarm (W6 TBR Abbruch) auslöst, der durch starke Vibrationen mittgeteilt wird.
* Manchmal kann es vorkommen, dass AAPS einen W6 TBR Abbruch Alarm nicht selbst quittiert, dann muss der Benutzer die Warnung selbst bestätigen entweder durch bestätigen des Alarms auf der Pumpe oder durch den Refresh Button im Combo Tab die Warnung an AAPS übergeben, damit AAPS die Warnung bestätigen kann.
* Die Stabiltät der Bluetooth Verbindung variiert je nach verwendetem Telefon stark, dies kann zu "pump unreachable" Alarmen führen, und verhindern, dass die Verbindung zur Pumpe hergestellt werden kann. Wenn dieses Verhalten auftritt, prüfe ob
a) BT auf dem Telefon eingeschaltet ist
b) Refresh im Combo Tab von AAPS die Verbindung wieder herstellt.
Versuche das Telefon neu starten, wenn die Schritte a und b nicht erfolgreich waren.
Wenn alles oben genannte nicht hilft, dann kann es nötig sein auf der Pumpe einen Knopf zu drücken (dadurch wird BT auf der Pumpe gestoppt und neu gestartet).
Derzeit ist nicht absehbar, dass dieses Verhalten verhindert werden kann. Wenn diese Fehler öfter auftreten, dann besteht die derzeit einzige Lösung in der Verwendung eines Telefons, von dem bekannt ist, dass es zuverlässig mit der Combo unter AAPS zusammenarbeitet (unten gibt es eine kurze Liste von Telefonen).
*Bolusabgabe direkt an der Pumpe wird von AAPS erkannt (immer wenn AAPS sich mit der Pumpe verbindet), im ungünstigsten Fall, kann das aber bis zu 20 minuten dauern. Bevor mittels AAPS die Basalrate über 100% erhöht wird oder ein Bolus abgegeben wird überprüft AAPS ob ein Bolus an der Pumpe abgegeben wird. Es wird dennoch empfohlen AAPS für alle Interaktionen mit der Pumpe zu verwenden.
* Das Setzen einer TBR direkt auf der Pumpe ist im closed Loop Betrieb nicht nötig und sollte im Allgemeinen nicht vorgenommen werden. Das Erkennen einer manuell gesetzten Basalrate kann bis zu 20 min Dauern und wird bei der Berechung auch nur ab dem Zeitpunkt verwendet, zu dem die TBR von AAPS eingelesen wird. Das führt dazu, dass die im Körper befindliche Insulinmenge (IOB) falsch berechnet wird.

## Setup

- Configure the pump using 360 config software.
  - Required (marked green in screenshots):
    - Set/leave the menu configuration as "Standard", this will show only the supported
      menus/actions on the pump and hide those which are unsupported (extended/multiwave bolus,
      multiple basal rates), which cause the loop functionality to be restricted when used because
      it's not possible to run the loop in a safe manner when used.
    - Verify the _Quick Info Text_ is set to "QUICK INFO" (without the quotes, found under _Insulin Pump Options_).
    - Set TBR _Maximum Adjustment_ to 500%
    - Disable _Signal End of Temporary Basal Rate_
    - Set TBR duration step-size to 15 min
    - Enable Bluetooth
  - Recommended (marked blue in screenshots)
    - Set low cartridge alarm to your liking
    - Configure a max bolus suited for your therapy to protect against bugs in the software
    - Similarly, configure maximum TBR duration as a safeguard. Allow at least 3 hours, since
      the option to disconnect the pump for 3 hours sets a 0% for 3 hours.
    - Enable key lock on the pump to prevent bolusing from the pump, esp. when the
      pump was used before and quick bolusing was a habit.
    - Set display timeout and menu timeout to the mininum of 5.5 and 5 respectively. This allows the AAPS to
      recover more quickly from error situations and reduces the amount of vibrations that can occur during
      such errors

![](https://github.com/jotomo/AndroidAPS/blob/combo/documentation/images/combo-menu-settings.png)
![](https://github.com/jotomo/AndroidAPS/blob/combo/documentation/images/combo-pump-options-settings.png)
![](https://github.com/jotomo/AndroidAPS/blob/combo/documentation/images/combo-tbr-settings.png)
![](https://github.com/jotomo/AndroidAPS/blob/combo/documentation/images/combo-bolus-settings.png)
![](https://github.com/jotomo/AndroidAPS/blob/combo/documentation/images/combo-insulin-settings.png)

- Install AndroidAPS as described in the wiki http://wiki.AndroidAPS.org and use the `combo` branch.
- Make sure to read the wiki to understand how to setup AndroidAPS.
- Select the MDI plugin in AndroidAPS, not the Combo plugin at this point to avoid the Combo
  plugin from interfering with ruffy during the pairing process.
- Follow the link http://ruffy.AndroidAPS.org and clone ruffy via git. Use the same branch as you use for
  AndroidAPS, currently there is only the `combo` branch.
- Pair the pump using ruffy. If it doesn't work after multiple attempts, switch to the `pairing` branch,
  pair the pump and then switch back the original branch.
  If the pump is already paired and can be controlled via ruffy, installing the `master` branch is sufficient.
  Note that the pairing processing is somewhat fragile (but only has to be done once)
  and may need a few attempts; quickly acknowledge prompts and when starting over, remove the pump device
  from the bluetooth settings beforehand. Another option to try is to go to the bluetooth menu after
  initiating the pairing process (this keeps the phone's bluetooth discoverable as long as the menu is displayed)
  and switch back to ruffy after confirming the pairing on the pump, when the pump displays the authorization code.
  When AAPS is using ruffy, the ruffy app can't be used. The easiest way is to just
  reboot the phone after the pairing process and let AAPS start ruffy in the background.
- Before enabling the Combo plugin in AAPS make sure your profile is set up
  correctly and your basal profile is up to date as AAPS will sync the basal profile
  to the pump. Then activate the Combo plugin.

## Usage

- Keep in mind that this is not a product, esp. in the beginning the user needs to monitor and understand the system,
  its limitations and how it can fail. It is strongly advised NOT to use this system when the person
  using it is not able to fully understand the system.
- Read the OpenAPS documentation https://openaps.org to understand the loop algorithm AndroidAPS
  is based upon.
- Read in the wiki to learn about and understand AndroidAPS http://wiki.AndroidAPS.org
- This integration uses the same functionality which the meter provides that comes with the Combo.
  The meter allows to mirror the pump screen and forwards button presses to the pump. The connection
  to the pump and this forwarding is what the ruffy app does. A `scripter` components reads the screen
  and automates inputing boluses, TBRs etc and making sure inputs are processed correctly.
  AAPS then interacts with the scripter to apply loop commands and to administer boluses.
  This mode has some restrictions: it's comparatively slow (but well fast enough for what it is used for),
  and setting a TBR or giving a bolus causes the pump to vibrate.
- The integration of the Combo with AndroidAPS is designed with the assumption that all inputs are
  made via AndroidAPS. Boluses entered on the pump directly will be detected by AAPS, but it can take
  up to 20 min before AndroidAPS becomes aware of such a bolus. Reading boluses delivered directly on
  the pump is a safety feature and not meant to be regularly used (the loop requires knowledge of carbs
  consumed, which can't be entered on the pump, which is another reason why all inputs should be done
  in AndroidAPS). 
- Don't set or cancel a TBR on the pump. The loop assumes control of TBR and cannot work reliably otherwise, determining the start time of an active TBR is not possible.
- The pump's first basal rate profile is read on application start and is updated by AAPS.
  The basal rate should not be manually changed on the pump, but will be detected and corrected as a safety
  measure (don't rely on safety measures by default, this is meant to detect an unintended change on the pump).
- It's recommended to enable key lock on the pump to prevent bolusing from the pump, esp. when the
  pump was used before and quick bolusing was a habit.
  Also, with keylock enabled, accidentally pressing a key will NOT interrupt active communication
  between AAPS and pump.
- When a BOLUS/TBR CANCELLED alert starts on the pump during bolusing or setting a TBR, this is
  caused by a disconnect between pump and phone. AAPS will try to reconnect and confirm the alert
  and then retry the last action (boluses are NOT retried for safety reasons). Therefore,
  such an alarm shall be ignored (cancelling it is not a big issue, but will lead to the currently
  active action to have to wait till the pump's display turns off before it can reconnect to the
  pump). If the pump's alarm continues, the last action might have failed, in which case the user
  needs to confirm the alarm.
- When a low cartridge or low battery alarm is raised during a bolus, they are confirmed and shown
  as a notification in AAPS. If they occur while no connection is open to the pump, going to the
  Combo tab and hitting the Refresh button will take over those alerts by confirming them and
  showing a notification in AAPS.
- When AAPS fails to confirm a TBR CANCELLED alert, or one is raised for a different reason,
  hitting Refresh in the Combo tab establishes a connection, confirms the alert and shows
  a notification for it in AAPS. This can safely be done, since those alerts are benign - an
  appropriate TBR will be set again during the next loop iteration.
- For all other alerts raised by the pump: connecting to the pump will show the alert message in
  the Combo tab, e.g. "State: E4: Occlusion" as well as showing a notification on the main screen.
  An error will raise an urgent notification. AAPS never confirms serious errors on the pump,
  but let's the pump vibrate and ring to make sure the user is informed of a critical situation
  that needs action.
- After pairing, ruffy should not be used directly (AAPS will start in the background as needed),
  since using ruffy at AAPS at the same time is not supported.
- If AAPS crashes (or is stopped from the debugger) while AAPS and the pump were communicating (using
  ruffy), it might be necessary to force close ruffy. Restarting AAPS will start ruffy again.
  Restarting the phone is also an easy way to resolve this or you don't know how to force kill
  an app.
- Don't press any buttons on the pump while AAPS communicates with the pump (Bluetooth logo is
  shown on the pump).

## Getestete Mobiltelefone

Siehe https://github.com/MilosKozak/AndroidAPS/wiki/Accu-Chek-Combo-Pump#tested-phones