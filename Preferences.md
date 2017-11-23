## Password for settings
This allows you to set a password in order to prevent accidental or unauthorised changes to Preferences. After you enter a password here you will be required to enter it in order to access Preferences.  To remove the password option then when within the Preferences delete the text within this field.
## Patient age
Algorithms are different based on patient age so select Child, Teenage or Adult here.
## General
* Select your language here.  If your language is not available, or not all of the words translated then feel free to make some suggestions.  The translation files are found here: [App >
 Src > Main > Res > Values > Strings](https://github.com/MilosKozak/AndroidAPS/blob/dev/app/src/main/res/values/strings.xml) or ask in the [gitter chatroom](https://gitter.im/MilosKozak/AndroidAPS).
* Quick Wizard settings allows you to add a quick button for a frequent snack or meal, enter your decided carb details and on the homescreen if you select the quick wizard button it will calculate and bolus for those carbs based on your current ratios (not taking into account blood glucose value or insulin on board though).
## Careportal
'Entered by' is the text displayed in your nightscout careportal 'entered by' field.  Set this to something meaningful to you, whether it is the app name, the persons name or the phone name (for example if you are using AndroidAPS as NS Client on a phone that is not the patients phone you may wish to distinguish between phone owners here).
## Treatments safety
* Max allowed bolus [U]
This is the maximum amount of bolus insulin that AAPS is allowed to deliver. This setting exists as a safety limit to prevent the delivery of a massive bolus due to accidental input or user error. It is recommended to set this to a sensible amount that corresponds roughly to the maximum amount of bolus insulin that you are ever likely to need for a meal or correction dose. This restriction is also applied to the results of the Bolus Calculator.
## Loop
You can toggle between open and closed looping here.  Open looping means TBR suggestions are made based on your data and appear as a notification but you must manually choose to accept them and manually enter them into your pump.  Closed looping means TBR suggestions are automatically sent to your pump without confirmation or input from you.  The homescreen will display in the top left corner whether you are open or closed looping, and pressing and holding this homescreen button will also allow you to toggle between the two.
## Profile
Selecting 'Sync profile to pump' will send your current AndroidAPS profile to the pump as basal profile 1 which means than should AndroidAPS stop working or loose connection with the pump then your pump will revert to the same profile as default rather than you having to manually enter it into the pump.  For more information on profiles see [[Working with profiles in 1.5]].
## Pump settings
The options here will vary depending on which pump driver you have selected in 'Config Builder'.  Pair and set your pump up according to the [[DanaR Insulin Pump]] instructions where relevent.
## NS Client
* Set your 'nightscout URL' here (https://yourwebsitename.herokuapp.com or https://yourwebsitename.azurewebsites.net), and the 'API secret' (a 12 character password recorded in your heroku or azure variables).  This enables data to be read and written between both the nightscout website and AndroidAPS.  Double check for typos here if you are stuck in Objective 1.
* 'Log app start to nightscout' will record a note in your careportal entries every time the app is started.  The app should not be needing to start more than once a day, more frequently than this suggests a problem.  
* 'Enable local broadcasts' will share your careportal data to other apps on the phone such as xdrip.  
* 'Alarm options' allows you to select which default nightscout alarms to use through the app, to set the alarm values amend your [heroku or azure variables](http://www.nightscout.info/wiki/welcome/website-features#customalarms).
## SMS Communicator
This setting allows remote control of the app by texting instructions to the patients phone which the app will follow such as suspending loop, or bolusing.  Further information is described in [[SMS Commands]].
## Other
* You can set defaults for your temp targets here, for more information see [[Open APS features]].  
* You can set default prime amounts - this will prime the pump the value specified and this insulin is counted as used from the reservoir but not counted in IOB calculations. See the instruction booklet in your cannula box for how many units should be primed depending on needle length and tubing length.
* You can change the display on the homescreen and watch for the values that are in range.  Note that this is just how the graphs look and doesn't impact on your target or calculations.
* 'Shorten tab titles' allows you to see more tab titles on screen, for example the 'Open APS' tab becomes 'OAPS', 'Objectives' becomes 'Obj' etc.
## Advanced Settings ``requires more work
* OpenAPS MA
  * Always use short average delta instead of...
Enabling this setting is useful when you are using data from unfiltered sources such as xDrip+, as opposed to filtered sources such as an official Dexcom Receiver. Filtered data appears to be smooth, whereas unfiltered data can appear to be jumpy. This unfiltered data could cause AndroidAPS to apply Temporary Basal Rate changes more frequently than are really needed, as the OpenAPS algorithm reacts to the jumpy data. With this setting enabled, the OpenAPS algorithm will use the Short Average Delta (the average change in blood glucose over the past 15 minutes) instead of the last blood glucose reading received. This effectively has a "smoothing" effect on the data and attempts to compensate for any jumpy readings.

Users of Abbot Freestyle Libre sensors collecting their glucose data via devices such as LimiTTers may find this setting provides better results with AAPS.

For further tips regarding data smoothing when using xDrip+ as the data source, see [Smoothing Blood Glucose Data in xDrip+](https://github.com/MilosKozak/AndroidAPS/wiki/Smoothing-blood-glucose-data-in-xDrip).
## Wear Settings
For more information on the wear watchface settings see [[Watchfaces]].