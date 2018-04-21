# Work in Progress

- [ ] Add to _Usage_ section in sidebar when ready
- [ ] Extend to explain the entire dialog, including use cases e.g. for Hypo TT (counteract overrcorrection from loop with fast-acting carbs)?
- [ ] Maybe better screenshots showing a realistic example

The _Carbs_ button on the overview tab has a _duration_ field since version 1.60 if engineering mode is enabled. 
This can be used when meals are longer, like a brunch, or the consumed carbs are longer acting, like with fat and protein-rich meals. The _time_ field allows shifting the carbs to have them start sooner or later:

<img src="https://user-images.githubusercontent.com/1732305/38613967-e2bd719a-3d8b-11e8-8c5f-b3c96607ad78.png" width=400>

If a duration is specified, the entered carbs will be created over the specified time, split up into smaller carbs every 15m:

<img src="https://user-images.githubusercontent.com/1732305/38613976-e52547c8-3d8b-11e8-91ff-4fbba4016e9b.png" width=400>

Carb entries which are in the future are coloured in dark orange:

<img src="https://user-images.githubusercontent.com/1732305/38613978-e6d1748e-3d8b-11e8-9d62-154fe73443da.png" width=400>

***
This, in general, aligns better with how carbs affect blood glucose for the meals described. This will allow the loop to enact SMBs for those carbs to prevent a raise in blood glucose typically seen with those meals. You can think of it as an extended bolus, but rather than delivering a fixed bolus, the loop is informed about the carbs and can dynamically bolus for it. This requires the OpenAPS SMB plugin to be used, with SMBs enabled as well as the _Enable SMB with COB_ being enabled.
A scenario e.g. for a Pizza might be to give a partial bolus up front via the _calculator_ and then use the _carbs_ button to enter the remaining carbs for a duration of 4-6 hours, starting after 1 or 2 hours. You'll need to try out and see which concrete values work for you of course. You might also carefully adjust the setting _max minutes of basal to limit SMB to_ to make the algorithm more or less aggressive.
With low carb, high fat/protein meals it may be enough to only use _Extended carbs_.