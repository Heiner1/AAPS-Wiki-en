New users often ask why AndroidAPS is high temping just after… or low temping when bloods are….  Here are a few steps you can take to help you understand what the algorithm is doing, why, and how you can work with this rather than against it. 

First things first, the founding principle of closed looping is that your basal rate and carb ratio is accurate. The adjustments the closed loop can make for safety have been limited, which means that you don't want to waste the allowed dosing on correcting a wrong underlying basal or carb ratio. You can use autotune to consider a large pool of data to suggest whether and how basals and/or ISF need to be adjusted, and also whether carb ratio needs to be changed. Or you can test and set your basal the old fashioned way.

AndroidAPS isn't a secret black box, it always tells you what it is thinks is going to happen, what it wants to do, and what it is currently doing.  In the app you will find this on the OpenAPS (OAPS) tab, or in Nightscout (useful to check for historical data) you will find it by hovering over the OpenAPS pill, or in the day to day report hovering over the bg data if you have selected openaps.
_[screenshots]_

The Result box will tell you the following information:
*  Temp = type of temporary basal - always “absolute”
*  Bg = current blood glucose in mg/dl
*  Tick = change since last blood glucose in mg/dl
*  eventualBG = predicted value of blood glucose (based on openaps logic) after full effect of IOB
*  snoozeBG = predicted value of blood glucose adjusted for bolussnooze IOB [Units of bolus IOB, if duration of insulin activity (DIA) was half what you specified. Used to determine how long to avoid low-temping after a bolus while waiting for carbs to kick in].
*  predBGs =
   *  IOB = predictions based on insulin only 
   *  aCOB = predictions based on an assumed 10 mg/dL/5m carb (0.6 mmol/L/5m) absorption
   *  COB = predictions based on current carb absorption
*  COB = carbs on board
*  IOB = net insulin on board
*  Reason = summary of why the decision was made
*  Timestamp = date and time the algorithm (and reasons above) was last run
	
The Reason field gives you the most information.  It tells you _…still to write…_

Steps to help you understand why its not doing what you would expect:
*  Check the predictions: What does it predict your bloods will be?  Is this actually happening?  If your bloods are not doing what AndroidAPS predicts then look into the three pink prediction lines and 
   *  Remember it predicts until the end of your DIA so the graphic prediction line on the homepage may be shorter than the final prediction in the result box.  Is the IOB prediction line looking like you would expect?  Does the curve match the curve of your insulin?  Incorrect settings in both DIA, insulin curves could impact on this.
   *  Are there any factors you are aware of that AndroidAPS isn't that will impact on the bloods e.g. a big portion of protein and fat increasing the remaining COB? Or a bent cannula reducing the IOB?
*  Check any constraints: has dosing been limited by your max_IOB or max_daily_safety_multiplier or current_basal_safety_multiplier?  In the reason field it will tell you what temp basal it wants to give and what temp basal it has actually given.  If these do not match then it will tell you 'adjusting required rate' and which setting has limited it.