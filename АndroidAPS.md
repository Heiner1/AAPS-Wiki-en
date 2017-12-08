* В AndroidAPS, изберете Конфигурация (CONFIG BUILDER) и направете вашите предпочитания за програмата.
    * ПРОФИЛ:
      * NS Профил - програмата, а също така и помпата ще използва вашият профил от Найтскаут.
      * Обикновен профил - най-опростеният локален профил.
      * Локален профил - профил с повече възможности, който се настройва само в AndroidAPS, без възможност за избиране на различни варианти
      * Процентен профил - това също е локален профил, който се задава в AndroidAPS, но позволява лесно увеличаване и намаляване с определен процент (между 50 и 200%), а също така и отместване с определен часови интервал зададен от вас. При версия по-нова от 1.54 е препоръчително да не ползвате този тип профил (Процентен), а да превключите на **Локален** понеже цялата функционалност на първия е прехвърлена във втория.

ИНСУЛИН:
Бързодействащ инсулин - това са бързодействащи инсулини, като NovoRapid и Humalog

* Select Menu by tapping the 3 dots in the top right. Select Preferences.
* Select DanaR Bluetooth device, and click your DanaR serial number.
* Select Pump password, and input your password. (Default password is 1234)
* If you want AndroidAPS to allow basal rate above 200%, enable Use extended boluses for >200%.
* Input your value for DanaR profile settings.
[[https://github.com/MilosKozak/AndroidAPS/wiki/images/AndroidAPS1.png]]
* Exit Preferences, and go to DANAR tap. Click bluetooth icon in the top right to connect with DanaR pump.
* Go to Preferences, and input your value for OpenAPS MA field.
* Go to CONFIG BUILDER tap and enable xDrip, OpenAPS MA, Loop and Profile you want to use.
[[https://github.com/MilosKozak/AndroidAPS/wiki/images/AndroidAPS2.png]]
* Go to OVERVIEW tap and check if your BG value is read from xDrip.
* Go to OBJECTIVES tap, and start to learn basic of OpenAPS by clearing objectives.
[[https://github.com/MilosKozak/AndroidAPS/wiki/images/AndroidAPS3.png]]
* Once you have been looping for 3 consecutive nights please fill [this form](http://bit.ly/nowlooping) in selecting Android APS as your type of DIY Loop Software.  Your information will not be shared in any way. You can indicate your preferred privacy levels in the form.