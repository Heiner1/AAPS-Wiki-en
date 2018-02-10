# **WORK IN PROGRESS**

**This software is part of a DIY solution and is not a product, but
requires YOU to read, learn and understand the system and how to use it.
It is not something that does all your diabetes management for you, but
allows you to improve your diabetes and quality of life significantly
if you're willing to put in the time required. Don't rush into it,
but allow yourself time to learn. You alone are responsible for what
you do with it.**

## Hardware requirements

- A Roche Accu-Chek Combo (any firmware, they all work)
- A Smartpix or Realtyme device together with the 360 Configuration
  Software to configure the pump.
  Roche sends out Smartpix devices and the configuration software
  free of charge to their customers upon request.
- A compatible phone: An Android phone with a phone running LineageOS 14.1 (formerly CyanogenMod) or Android 8.1 (Oreo). A list of phones can be found here https://docs.google.com/spreadsheets/d/1-Im_rTkWPbk-Pl_hlnh-GhfZbAlXbh4PiLNnBJqGFyk/edit#gid=0. Please be aware that this is not complete list and reflects personal user experience. You are encouraged to also enter your experience and thereby help others (these projects are all about paying it foward).

  Be aware that while Android 8.1 allows communicating with the Combo, there are still issues with AAPS on 8.1.
  For advanced users, it is possible to perform the pairing on a rooted phone and transfer it to another rooted
  phone to use with ruffy/AAPS, which must also be rooted. This allows using phones with Android < 8.1 but
  has not been widely tested: https://github.com/gregorybel/combo-pairing/blob/master/README.md

## Limitations

- Extended bolus and multiwave bolus are not supported.
- Only one basal profile is supported.
- Setting a basal profile other than 1 on the pump, or delivering extended boluses or multiwave
  boluses from the pump interferes with TBRs and forces the loop into low-suspend only mode for 6 hours
  as the the loop can't run safely under those conditions.
- It's currently not possible to set the time and date on the pump, so daylight saving times
  changes have to be performed manually (disable automatic phone clock update in the evening and
  update change back in the morning while also updating the pump's clock to avoid an alarm during the night).
- Currently only basal rates in the range of 0.05 to 10 U/h are supported (this also applies when modifying
  a profile, e.g. when increasing to 200%, the highest basal rate must not exceed 5 U/h since it will be
  doubled. Similarly, when reducing to 50%, the lowest basal rate must be at least 0.10 U/h).
- If the loop requests a running TBR to be cancelled the Combo will set a TBR of 90% or 110%
  for 15 minutes instead. This is because cancelling a TBR causes an alert on the pump which
  causes a lot of vibrations.
- Occasionally (every couple of days or so) AAPS might fail to automatically cancel
  a TBR CANCELLED alert the user then needs to deal with (press the refresh button in AAPS
  to transfer the warning to AAPS or confirm the alert on the pump).
- Bluetooth connection stability varies with different phones, causing "pump unrechable" alerts, 
  where no connection to the pump is established anymore. If that error occurs, make sure Bluetooth 
  is enabled, press the Refresh button in the Combo tab to see if this was caused by an intermitted 
  issue and if still no connection is established, reboot the phone which should usually fix this. 
  There is another issue were a restart doesn't help but a button on the pump must be pressed (which 
  resets the pump's Bluetooth), before the pump accepts connections from the phone again. There is very 
  little that can be done to remedy either of those issues at this point. So if you see those errors 
  frequently your only option at this time is to get another phone that's known to work well with 
  AndroidAPS and the Combo, see the [Tested phones](https://github.com/MilosKozak/AndroidAPS/wiki/Accu-Chek-Combo-Pump#tested-phones) section at the end.
- Issuing a bolus from the pump will be detected (checked for whenever AAPS connects to the pump), but might take up to 20 minutes in the worst case. Boluses on the pump are always checked before a high TBR or a bolus issued by AAPS.
- Setting a TBR on the pump is to be avoided since the loop assumes control of TBRs. Detecting a new TBR on the pump might take up to 20 minutes and the TBR's effect will only be accounted from the moment it is detected, so in the worst case there might be 20 minutes of a TBR that is not reflected in IOB. 

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
  AndroidAPS, right now that's the `combo` branch, later on there will be the normal `master` and `dev` branches.
- Pair the pump using ruffy. If it doesn't work after multiple attempts, switch to the `pairing` branch,
  pair the pump and then switch back the original branch.
  If the pump is already paired and can be controlled via ruffy, installing the `combo` branch is sufficient.
  Note that the pairing processing is somewhat fragile (but only has to be done once)
  and may need a few attempts; quickly acknowledge prompts and when starting over, remove the pump device
  from the Bluetooth settings beforehand. Another option to try is to go to the bluetooth menu after
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

## Tested phones

Testing phones: use the phone with the Combo at least one week (better two weeks). Notice how often _pump unreachable_ alerts occur, which require either rebooting the phone or pressing a button on the pump. Only if you encounter none of these issues add the phone here with the comment "no issues". Otherwise add the rough frequency these errors occur.
- ZTE Axon 7 with G5 running official LineageOS 14.1: no issues
- Xiaomi Redmi 4x running unofficial LineageOS 14.1: no issues
- Samsung Galaxy S5 Mini with G5 running unofficial LineageOS 14.1: pump becomes unreachable every couple of days, requiring a button press on the pump.
- Samsung Galaxy S4 Mini, LineageOS 14.1: no issues
- Sony Z3 Compact with G5 running unofficial LineageOS 14.1: frequent connection problems
- Sony Xperia Z5 Compact with Libre+Nightrider; unofficial LineageOS 14.1: no issues
- Moto G 1st Gen running official LineageOS 14.1: no issues
- Moto G 2nd Gen LTE running official LineageOS 14.1: no issues
- Huawei P8 Lite running unofficial LineageOS 14.1: rare connection problems (approx. 1 per week) that can be resolved by pressing a button on the pump.