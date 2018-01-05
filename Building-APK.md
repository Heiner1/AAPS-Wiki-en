* Download the [AndroidAPS repository](https://github.com/MilosKozak/AndroidAPS) and extract the files or use git clone
![](https://github.com/RadoslavR/AndroidAPS/blob/master/Screenshot%202018-01-02%2008.32.12.png)
![](https://github.com/RadoslavR/AndroidAPS/blob/master/Screenshot%202018-01-05%2008.54.26.png)


* Run Android Studio and select 'Open an existing Android Studio project', selecting the location of the extracted files.

* Click on BuildVariants button on the bottom left of the Android Studio, and notice that you have several kinds of build types.


[[https://github.com/gempickfordwaugh/AndroidAPS/raw/b09d7dc444f59b799888bcd596e36e1d562a9674/fullwearcontrolrelease.png]] 

* Select the build type you want to build. There are different modular options, the different parts of the name are described below to help you choose, we recommend **bold** for default AndroidAPS app (**fullWearcontrolRelease**) or _italic_ for parents monitoring looping (_nsclientWearRelease_).
    * **full - full app**
    * _nsclient - downloads treatments from NS and uploads care portal entries (no looping, just monitors looping from elsewhere)_
    * openloop - just the OpenAPS part of the app (no pump driver)
    * pumpcontrol - just the DanaR remote control part of the app (no looping function, just for bolusing)<br><br>

    * Nowear - just phone app, doesn't include watch app
    * _Wear - includes android wear watch app for viewing_
    * **Wearcontrol - includes android wear watch app for controlling pump (e.g. temp targets and bolusing)**<br><br>

    * _**Release - should be the default choice**_
    * Debug - just for people coding

* Go to Build Menu and click on Generate Signed APK

* Set a keystore and password, if this is your first time then Create new, or fill in the details of your existing one.  For more information about using the keystore see [https://developer.android.com/studio/publish/app-signing.html#generate-key](https://developer.android.com/studio/publish/app-signing.html#generate-key)

[[https://github.com/gempickfordwaugh/AndroidAPS/raw/b09d7dc444f59b799888bcd596e36e1d562a9674/generate%20signed%20APK.png]]

*   Select the same build type as previous, select V1 (Jar Signature) and click Finish. 

[[https://github.com/gempickfordwaugh/AndroidAPS/raw/b09d7dc444f59b799888bcd596e36e1d562a9674/generate%20signed%20APK%20select%20buildtype%20v1.png]]

* Please wait for some time until the APK is created. You will get the pop-up below when the process is done.

[[https://github.com/MilosKozak/AndroidAPS/wiki/images/androidstudio3.png]]

* Click on 'Show in Explorer'. You'll find the APK is generated, sometimes it may take time to display.

* Copy the APK with the same finename as the buildtype you chose to your android phone, and install it.  If the apk does not install and you have an older version of AndroidAPS on your phone that was signed with a different key then you will need to uninstall this first, remember to export your settings if so.