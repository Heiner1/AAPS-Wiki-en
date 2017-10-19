The most stable version of AndroidAPS to use is that in the [Master branch](https://github.com/MilosKozak/AndroidAPS/tree/master).  It is advised to stay on the Master branch while you complete the Objectives and get practiced at looping.

However, the [Dev branch](https://github.com/MilosKozak/AndroidAPS/tree/dev) is a good place to see what features are being tested and to help iron out the bugs and give feedback on how the new features work in practice.  A short summary of some of the changes to old features or development of new features currently in the Dev branch is listed below, and links to any key issues known will be shared (if applicable).

**Build Variants**<br><br>
The number of build variants has been reduced to:
* full (i.e. recommendations automatically enacted in closed looping)
* openloop (i.e. recommendations given to user to manually enact)
* pumpcontrol (i.e. remote control for pump, no looping)
* nsclient (i.e. looping data of another user is displayed and careportal entries can be added)

Wear control can now be enabled or disabled direct from the phone settings; this gives parents more flexibility and control over the features their child can use.  The watch needs to be connected to the phone when toggling the settings - otherwise when it is connected again press re-sync from the watch or open the menu on the watch two times in a row.

**Profiles**<br><Br>
Circadian Percentage Profile (both timeshift and percentage) can now work with any Profile.  You no longer need to select "Circadian Percentage Profile" in the config builder, simply change profile using profile switch and you will also have the option to to change timeshift and/or percentage too.  This means you can easily tell AndroidAPS to decrease your profile (basal, bolus and sensitivity) by 30% for 6 hours for example when exercising without having to copy and paste profiles.
Switching profiles can also now be triggered by NS Client (picking it up from a Nightscout Careportal entry) or by the Profile Switch in AndroidAPS.  It means you can use conditional statement based systems (e.g. IFTTT/Automate/Tracker) to automatically change your profile for you based on other inputs (e.g. calendar entries, physical location).
<br><br><br>
If you find a bug or think something wrong has happened when using the Dev branch, then view the [issues tab](https://github.com/MilosKozak/AndroidAPS/issues) to check whether anyone else has found it, or add it yourself if not.  The more information you can share here the better (don't forget you may need to share your [log files](https://github.com/MilosKozak/AndroidAPS/wiki/Accessing-logfiles)).  The new features can also be discussed in the [gitter room](https://gitter.im/MilosKozak/AndroidAPS).