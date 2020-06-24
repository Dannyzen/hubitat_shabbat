# Hubitat Shabbat App

Uses the HebCal API to set a shabbat mode at the scheduled shabbat time for a given zip code.  

Changelog
--

* New June 2020: Virtual Device (Optional) has been added. If shabbat times are appropriately acquired at 8am, the device will turn on indicating the mode will change at shabbat time, but if the device is off after Friday at 8am, something is not working as it should and may need to be investigated.  Useful for rule machine triggered notifications that everything is going well. Also useful for avoiding the situation when your realize your house is still online 2 minutes before candlelighting :) see [rule_machine_virtual_switch.png](rule_machine_virtual_switch.png)

Supported Functionality
--
* Automates the process of setting a 'shabbat' mode for Shabbat & Yom Tov (really, whenever there is candle lighting time -- See "How it works").
* Supports local candle lighting time 

Recommended Practices
--

* Have a unique mode for shabbat and  _after_ shabbat. (I call these "Shabbat" and "After Shabbat")
* Create a "shabbat-on or shabbat-off group" for all the things you might want to turn off or turn on during shabbat.  It makes management and future proofing easier.
* Create a dashboard button that enables you to change the mode to Shabbat and to After Shabbat manually (In rare situations, it's possible for the scheduler to fail. (see "How it works")
* Consider creating a notification action when the mode changes to Shabbat. I toggle all the lights in my house at this time, it gives the family a friendly heads up.
* For full-proof confidence: It's best to check the app's status' page during the day on Friday or erev Yom Tov to make sure setChag has been set. You can do this by going to the app configuration page and clicking the 'gear' icon. 
* If for whatever reason the app fails to get candle lightning time, you can trigger it by changing & saving the zip code.

How it works
--
Every morning at 8am the app attempts to get candle lighting time for that day from hebcal.com. If candle lighting time is successfully obtained, the app runs the [setChag](https://github.com/Dannyzen/hubitat_shabbat/blob/master/shabbat-and-holiday-modes.groovy#L139) function for that time. This works great... most of the time (See Known Issues)


Known Issues
--
* Candle lightning time takes place during Chanukkah and the app pulls those times down. So, when it's Chanukkah time, Shabbat mode does initiate. (I don't have time to work around this but welcome community help!)
* If the 8am hebcal API call fails, the app won't pull shabbat time. 

FAQ
--

So for a 2-3 day holiday, the mode change happens 
daily or just once?
* If it's a 2 day holiday, the mode will: 

*Not change back to a non-holiday mode ("non-shabbat") at the end of the first day.  
*Attempt to change to holiday mode the night of the first day, since Yom Tov starts for day 2, on the night of the first day.

Does your app distinguish between Yom Tov and non-restrictive dates, like chol hamoed/Purim, etc?
* Theoretically, it can, because hebcal provides this data, at this time it does not because I haven't had a good enough reason to put time into it. Community help welcomed to make this happen.
