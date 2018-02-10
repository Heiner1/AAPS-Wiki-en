WORK IN PROGRESS

Die Software ist Teil einer DIY-Lösung(Do It Yourself = Eigenbau) und kein Produkt. Daher bist **Du **gefordert. **Du **musst lesen, lernen und verstehen was das System macht und wie du es bedienst.
Das System wird Dir nicht alle Schwierigkeiten Deiner Diabetestherapie abnehmen, aber wenn Du Willens bist die nötige Zeit zu investieren, dann kann es die Ergebnisse Deiner Therapie verbessern und die Lebensqualität erhöhen. Dir sollte klar sein, dass das System umso besser arbeitet, je besser Deine Therapiegrundeinstellung ist.
Hetz Dich nicht auch wenn andere Dir erzählen wie toll das alles ist. Nimm Dir Zeit zu lernen!
Du bist ganz alleine dafür verantwortlich was Du mit dem System machst.


Hardware requirements

    Eine Roche Accu-Chek Combo Pumpe (egal welche Firmware, es funktionieren alle)

    Einen Smartpix oder Realtyme Adapter und die Accu-Chek 360 Konfigurationssoftware umd die Pumpe zu konfigurieren. Kunden von Roche können die Software beim Kundendienst erfragen.

   Ein kompatibles Telefon: Ein Android Telefone mit LineageOS 14.1 (früher CyanogenMod) oder Android 8.1 (Oreo). Eine Liste gestester Telefone findet sich hier https://docs.google.com/spreadsheets/d/1-Im_rTkWPbk-Pl_hlnh-GhfZbAlXbh4PiLNnBJqGFyk/edit#gid=0. Die Liste ist nicht abschliessend und spiegelt nur die persönliche Erfahrung der Benutzer wieder. Bitte trage Deine Erfahrung in die Liste ein und hilf damit anderen. Die ganzen DIY Projekte funktionieren nur, wenn jeder etwas zurückgibt. 

    Vorsicht, obwohl man unter Android 8.1 mit der Combo Pumpe kommunizieren kann, gibt es noch Schwierigkeiten mit AAPS unter Android 8.1. Für Fortgeschrittene erfahrene Anwender gibt es noch die Möglichkeit Bluetooth Pairing zwischen Pumpe und einem gerooteten Android Telefon (Android 4.2) vorzunehmen und die Informationen dann auf ein anderes gerootetes Handy (Android > 5 ) zu übertragen, damit ruffy/AAPS auf dem zweiten Handy läuft.
Das erlaubt die Verwendung eines Android < 8.1 ist aber nicht großartig getestet und auch kein sehr verbreitetes Verfahren. https://github.com/gregorybel/combo-pairing/blob/master/README.md
Wenn Dir rooten/pairen und so weiter nichts sagen, dann ist die letzte Variante vermutlich nichts für Dich.

Beschränkungen

    Extended bolus and multiwave bolus are not supported.
    Es wird nur ein Basalprofil unterstützt.
    Setting a basal profile other than 1 on the pump, or delivering extended boluses or multiwave boluses from the pump interferes with TBRs and forces the loop into low-suspend only mode for 6 hours as the the loop can't run safely under those conditions.
    It's currently not possible to set the time and date on the pump, so daylight saving times changes have to be performed manually (disable automatic phone clock update in the evening and update change back in the morning while also updating the pump's clock to avoid an alarm during the night).
    Currently only basal rates in the range of 0.05 to 10 U/h are supported (this also applies when modifying a profile, e.g. when increasing to 200%, the highest basal rate must not exceed 5 U/h since it will be doubled. Similarly, when reducing to 50%, the lowest basal rate must be at least 0.10 U/h).
    If the loop requests a running TBR to be cancelled the Combo will set a TBR of 90% or 110% for 15 minutes instead. This is because cancelling a TBR causes an alert on the pump which causes a lot of vibrations.
    Occasionally (every couple of days or so) AAPS might fail to automatically cancel a TBR CANCELLED alert the user then needs to deal with (press the refresh button in AAPS to transfer the warning to AAPS or confirm the alert on the pump).
    Bluetooth connection stability varies with different phones, causing "pump unrechable" alerts, where no connection to the pump is established anymore. If that error occurs, make sure Bluetooth is enabled, press the Refresh button in the Combo tab to see if this was caused by an intermitted issue and if still no connection is established, reboot the phone which should usually fix this. There is another issue were a restart doesn't help but a button on the pump must be pressed (which resets the pump's Bluetooth), before the pump accepts connections from the phone again. There is very little that can be done to remedy either of those issues at this point. So if you see those errors frequently your only option at this time is to get another phone that's known to work well with AndroidAPS and the Combo (see the Tested phones section at the end).
    Issuing a bolus from the pump will be detected (checked for whenever AAPS connects to the pump), but might take up to 20 minutes in the worst case. Boluses on the pump are always checked before a high TBR or a bolus issued by AAPS.
    Setting a TBR on the pump is to be avoided since the loop assumes control of TBRs. Detecting a new TBR on the pump might take up to 20 minutes and the TBR's effect will only be accounted from the moment it is detected, so in the worst case there might be 20 minutes of a TBR that is not reflected in IOB.

Setup

    Configure the pump using 360 config software.
        Required (marked green in screenshots):
            Set/leave the menu configuration as "Standard", this will show only the supported menus/actions on the pump and hide those which are unsupported (extended/multiwave bolus, multiple basal rates), which cause the loop functionality to be restricted when used because it's not possible to run the loop in a safe manner when used.
            Verify the Quick Info Text is set to "QUICK INFO" (without the quotes, found under Insulin Pump Options).
            Set TBR Maximum Adjustment to 500%
            Disable Signal End of Temporary Basal Rate
            Set TBR duration step-size to 15 min
        Recommended (some marked blue in screenshots)
            Set low cartridge alarm to your liking
            Configure a max bolus suited for your therapy to protect against bugs in the software
            Similarly, configure maximum TBR duration as a safeguard. Allow at least 3 hours, since the option to disconnect the pump for 3 hours sets a 0% for 3 hours.
            Enable key lock on the pump to prevent bolusing from the pump, esp. when the pump was used before and quick bolusing was a habit.
            Set display timeout and menu timeout to the mininum of 5.5 and 5 respectively. This allows the AAPS to recover more quickly from error situations and reduces the amount of vibrations that can occur during such errors
