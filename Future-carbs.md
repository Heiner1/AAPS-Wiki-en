The _Carbs_ button on the overview tab has a _duration_ field since version 2.0. 
This can be used when meals are longer, like a brunch, or the consumed carbs are longer acting, like with fat and protein-rich meals. The _time_ field allows shifting the carbs to have them start sooner or later:

<img src="https://1.bp.blogspot.com/-gnWKSBIBO2g/WuTPV0Rya3I/AAAAAAAAAEg/BvqiZYrsuKcgbny5t1sHWlPS6feWq-xEwCLcBGAs/s1600/Screenshot_20180427-144305.png" width=400>

If a _duration_ is specified, the entered carbs will be created over the specified time, split up into smaller carbs every 15m:

<img src="https://4.bp.blogspot.com/-sgc9XdUeaoQ/WuTPXxfaIuI/AAAAAAAAAEk/p7toa_aq_oIWWTnzoQFUPHt4JdPkaXrwwCLcBGAs/s1600/Screenshot_20180427-144324.png" width=400>

Carb entries which are in the future are coloured in dark orange:

<img src="https://user-images.githubusercontent.com/1732305/38613978-e6d1748e-3d8b-11e8-9d62-154fe73443da.png" width=400>

***
A way to handle fat and protein with that feature is described here: https://adriansloop.blogspot.co.at/2018/04/page-margin-0.html
***

This, in general, aligns better with how carbs affect blood glucose for the meals described. This will allow the loop to enact SMBs for those carbs to prevent a raise in blood glucose typically seen with those meals. You can think of it as an extended bolus, but rather than delivering a fixed bolus, the loop is informed about the carbs and can dynamically bolus for it. This requires the OpenAPS SMB plugin to be used, with SMBs enabled as well as the _Enable SMB with COB_ being enabled.
A scenario e.g. for a Pizza might be to give a partial bolus up front via the _calculator_ and then use the _carbs_ button to enter the remaining carbs for a duration of 4-6 hours, starting after 1 or 2 hours. You'll need to try out and see which concrete values work for you of course. You might also carefully adjust the setting _max minutes of basal to limit SMB to_ to make the algorithm more or less aggressive.
With low carb, high fat/protein meals it may be enough to only use _Extended carbs_.
Generated carbs with a date in the future are shown in brackets where COB is displayed (overview screen, watchface).