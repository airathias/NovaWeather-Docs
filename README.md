# Nova Weather - Harmony Mod for RUST

**Nova Weather**  is a drop-in replacement for Rust’s native server-side weather system. It is very customizable with unique features such as timelined profiles with events, and exceptional features that make it stand out such as support for zone-specific weather systems.

**Please note: This mod has no required dependencies, and can work out of the box  without Oxide. Only if you need zone support will you need Oxide and the ZoneManager plugin.**

# Features

![Timelines](https://hypernova.gg/vendor-products/harmony/novaweather/Feature_Timelines.png)

First off, we have Profile Timelines. This allows you to carefully construct your weather system by introducing elements staggered instead of all at once. For example; you could make a heavy rain storm by first making some clouds, then 30 seconds later darkening them, and when they’re done, slowly start rain that increases over 5 minutes until it’s at full strength.

You can play with about 20 weather properties ranging from cloud coverage to fogginess to windspeed, and even override temperatures.


![Timelines](https://hypernova.gg/vendor-products/harmony/novaweather/Feature_Zones.png)

For the first time, you can now have several separate weather systems active in your world using **Nova Weather**’s support for the ZoneManager plugin. You could make it rain on one island, and make it tropical on another. You could create zones for bosses where the sky darkens with thunderclouds the closer you get, or you could make your admin crib always sunny while the rest of the world is experiencing heavy rain. The possibilities are endless.


![Timelines](https://hypernova.gg/vendor-products/harmony/novaweather/Feature_Timed_Commands.png)

Not only are you able to use the Profile Timelines feature to create beautiful and realistic weather patterns, you can also make things happen based on whatever weather you have running.

Using the timeline, you can create a property element or you can create a command element. If you create a command element and place it on the 30 second mark in your timeline, the command will execute when 30 seconds have elapsed in that profile.

Want to spawn a boss when the thunder starts in a thunderstorm? Want to start an event when the rain stops? Want to give everyone some currency when you’ve had fog on for 10 minutes?! You can do that with scheduled commands!


![Timelines](https://hypernova.gg/vendor-products/harmony/novaweather/Feature_Share_profiles.png)

All weather systems work on a few simple concepts, and the most important of those are Profiles. Profiles determine what should be shown in the world. You’ll have a profile for Clear, Rain, Fog, etc. These profiles live in your configuration folder as separate files, and are completely interchangeable.

Created a kickass weather profile but hate the hassle of having to mix and match your config files? Just drop ‘em your profile files. They can just drag-and-drop them into their profiles folder, and they’re immediately usable. Share away!


![Timelines](https://hypernova.gg/vendor-products/harmony/novaweather/Feature_Advanced_Options.png)

With advanced features comes some advanced configuration. We’ve tried to make it as simple as possible though, and in the Configuration chapter below we explain what everything does. There’s all sorts of settings to make your weather look amazing, or to optimize the weather system’s performance for lower end machines. You can choose whether or not to use ZoneManager support, you can tweak the amount of times a second the system updates, etc. With a ton of RCON Commands included (20+!) you can even do most of it without ever looking at a JSON file.

The mod installs with a very comprehensive default configuration, created to mimic the native weather system with a bit of a makeover on install so you can just install and forget about it. The default profiles have timelines, and tweaked load chances to bring back some good looking weather types.



# Commands


**Nova Weather**  offers you a ton of commands to make your life as an admin easier, and to give you full control over your server’s weather. Don’t like a particular profile right now? Skip it! Wanna show off your profile but the fun only starts at the 1-minute mark? Skip to that moment in the timeline! **All commands are to be executed from the RCON or Server Console, not from in-game!**

All commands must start with either ‘novaweather.’ Or ‘nw.’. The list below uses the former for clarity, but you can use ‘nw.’ As a substitute to shorten your commands.

Arguments indicated with “<argument>” are mandatory for use with the command, while “(argument)” indicates an optional argument.

Please note: To be able to use any of the zone-related commands you need to have Oxide installed and have loaded the ZoneManager plugin.

Below you’ll find a list of all commands available with a short description.

### Basic commands

    novaweather.reload

Reloads the mod and will reload all profiles from disk, as well as check for the existence of ZoneManager zones. If you’ve purchased or downloaded profiles into your Profiles folder, reload the mod to have it take effect.

    novaweather.report (climate)

Reports the current weather conditions for all climates if the optional climate argument is not set. If it is, will limit the report to just that climate.

    novaweather.tickrate (number)

If no number is set, will return the current tick rate. If a number is passed, will set the tick rate to that number. The tick rate determines how often the weather system calculates and updates, with a lower number meaning more often. It’s basically saying “Update every <number>th frame”, with 1 being the lowest possible number and 50 being the highest. The lower the number, the smoother the transitions.

### Climate-related commands

    novaweather.globalclimate (climate)

If the climate argument is set, will set the global weather system’s climate to that climate. If the climate argument is not set, will return the name of the climate currently assigned to global weather.

    novaweather.load <climate> <profile> (transition)

Used to forcefully load a given profile to the climate immediately. If a numeric transition argument is passed, it will override the profile’s set transition time. “nw.load default default_clear 10” will load the default_clear profile and override the transition to 10 seconds to speed up the appearance of the profile.

    novaweather.loadnext <climate> <profile>

Will forcefully set the next profile for a climate. When the current weather profile reaches its’ end, the next profile is automatically loaded.

    novaweather.next <climate> (transition)

Forcefully ends the currently active profile’s timeline and loads in the next profile in the queue. If a numeric transition argument is passed, it will override the profile’s set transition time.

    novaweather.pause <climate>

Pauses the timeline for the provided climate. Pausing a climate will effectively freeze the current weather in its’ current state indefinitely until unpaused.

    novaweather.unpause <climate>

The ‘counter charm’ to the pause command. Unpauses the provided climate’s timeline (if it is paused).

    novaweather.skipto <climate>  <seconds>

Skip the current profile’s timeline to the provided seconds mark. If you enter a seconds mark greater than the timeline’s duration, it will skip it to the last frame effectively ending the profile’s timeline.

    novaweather.listclimates

Presents you with a neat list of all running climates and their status and a list of all assigned profiles.


### Zone-related commands

    novaweather.disablezones

Disables the ZoneManager support altogether. Will deactivate all non-global climates to save processing power.

    novaweather.enablezones

Basically the ‘counter charm’ to disablezones. Re-enables all disabled zones and boots up all non-global climates if any exist.

    novaweather.disablezone <zone>

Disables a single zone’s overrides. That’s about it.

    novaweather.enablezone <zone>

The brother-command of the above mentioned one. Enables the zone again.

    novaweather.showzone <zone>

More of a debug function, shows the wireframe for the given zone as if you’re editing it with ZoneManager. Good for determining a zone’s transition buffer zone.

    novaweather.zoneclimate <zone> (climate)

This is a big one. This will do a few things based on the provided arguments;

- If the climate argument is set and the zone is already registered with Nova Weather, it’ll change that zone’s climate and load it up immediately.

- If the climate is set and the zone is not already registered, it will register it and set the zone’s climate and load it up.

- If the climate argument is not set but the zone is registered, will return that zone’s set climate.

```
novaweather.removezone <zone>
```

Contrary to what you may think, this does not remove the actual ZoneManager zone. It just removes it from Nova Weather’s configuration and thus removes any zone overrides. This is permanent, if you’re just wanting to temporarily disable it use the ‘disablezones’ command listed above.

    novaweather.listzones

Lists all zones that are configured within Nova Weather with their status and climate.

### Profile-related commands

    novaweather.getprofile <climate>

Returns the name of the currently active profile for the given climate.

    novaweather.assignprofile <climate> <profile> (chance)

Adds a profile to a climate’s profile list to be included in rotation. If the chance argument is set, will override the default value of “100”. Note that “chance” doesn’t literally mean a chance %, it’s a weight to make a weighted random, just named “chance” to make sure people understand its’ intended use.

    novaweather.unassignprofile <climate> <profile>

The antithesis of the above-mentioned command. Will remove the profile from the climate’s profile rotation permanently.

    novaweather.setprofilechance <climate> <profile> <chance>

Sets the chance (weight) for the given profile in the context of the given climate’s list of profiles.

    novaweather.listprofiles

Lists all profiles loaded into Nova Weather’s memory. If you just created a profile file and don’t see it listed in this list, reload the plugin using the reload command in this list and try again.


# Configuration
**Nova Weather**’s configuration is pretty in-depth but we’re going to try to make it as painless as possible.

There’re two distinct types of configuration file for this mod, and those are the singular Configuration.json file and the individual Profile files. We’ll go over both in this section. All of Nova Weather's configuration files can be found in:

    ROOT / HarmonyMods_Data / NovaWeather (/ Profiles)

Before diving into these options, a few key concepts need to be clear for you to fully understand all the ways you can customize your server’s weather.

**Profiles**
Profiles are separate files with properties. They contain all actual weather data such as rain level, cloud coverage, etc. It does not do anything in and of itself, it's just basically a timeline that shows the climate what weather to present.

**Climates**
Second, there’s Climates. Climates are each individual and isolated weather systems, and are assigned one or more profiles to cycle through. They read the profile data and make all calculations for transitions, timelines, etc. They’re the brain of the operation.

**Zones**
Lastly there’s Zones. A zone is a ZoneManager zone that's registered with Nova Weather, and contains information like the zone ID and the climate that should be presented to the clients present within that zone. In and of itself this doesn't to anything, it just tells us to override the global weather climate with another climate.

Climates all cycle continuously in the background. Applying a climate to a zone doesn't change the climate at all, it just sort of subscribes to it. The climate is always telling the mod "Hey man, rain should be 1. wind should be 0". It doesn't care if anything's listening.

The zone can then sort of connect to that, and hear what the climate is saying, and then show that to the player. This makes it so you can have 10 zones that share 1 climate, saving a ton of processing power.


## Configuration files: Configuration.json**
All right, let’s dive into our first bit of configuration. We’ll first take a look at Configuration.json. Note that this config is subject to change, and the image below may not be a fully accurate depiction of the current state of the config file structure.

[![Nova-Weather-config-file.thumb.png.e7647c3abadfa06c6b019c5c1b71a899.png](https://codefling.com/uploads/monthly_2022_10/Nova-Weather-config-file.thumb.png.e7647c3abadfa06c6b019c5c1b71a899.png)](https://codefling.com/uploads/monthly_2022_10/Nova-Weather-config-file.png.5de9d9e9784c11ffe288bebd9c82559f.png)

    Modification enabled (true/false)

A Boolean to turn the mod on or off without having to unload it. Will enable the native weather system if set to false.

    Enable debug logs (true/false)

Will print quite verbose logs, meant to provide the developer more insight into potential problems. If you’re contacting support, make sure you include logs with this set to true.

    Global Options -> Pause weather if server empty (true/false)

Pauses all climates’ timelines to halt processing, since nobody’s there to enjoy it anyway. I can’t think of a real reason to set this to false unless its for testing purposes, but you have the option to.

    Global Options -> Global weather climate

Determines what climate will be applied to the global weather. Speaks for itself.

    ZoneManager options -> Use ZoneManager zones (true/false)

If set to true, this will apply (a) climate(s) to the zone(s) in the zone climates list. If set to false, this will completely disable all zone functionality and will limit the mod to only global weather.

    ZoneManager options -> ZoneManager zone climates

This is where you register and modify zone information. A zone can be disabled individually, have a climate set, and have a modified transition buffer. More on that below.

    ZoneManager options -> ZoneManager zone climates -> Enabled (true/false)

Enables or disables this particular zone from having a climate override.

    ZoneManager options -> ZoneManager zone climates -> Climate

The climate that should be shown to the clients within that zone.

    ZoneManager options -> ZoneManager zone climates -> Zone transition buffer percentage (1-100)

The percentage of the zone’s radius which should be used as a transition buffer. When you enter a zone, you don’t want to instantly have another weather type pop into existence. This is where the zone transition buffer saves the day; the weather types are gradually transitioned between until you’re well and proper into the zone. If you put this at 50%, you’ll see the transition happen for half of the zone. After halfway into the zone, you’ll see no trace of the “outside” climate and will just see the zone climate.

    ZoneManager options -> ZoneManager zone climates -> Zone transition buffer max. Size (meters)

With this you can put an absolute limit on the transition buffer size. This works best if you don’t exactly know the dimensions of the zone(s) you’ll be placing. This makes it so that the transition buffer will not go past the given number of meters past the zone’s border. So, if you set the buffer percentage to 50%, but set the max. meters to 10, the buffer will either go to 50% if it’s shorter than 10m, or it will cap at 10m.

See the graphic below for a visual representation, with “%” meaning the buffer zone percentage.

[![Nova-Weather-zone-buffer-explanation.png.9ff2be4e8387080905e2a5850ca660da.png](https://codefling.com/uploads/monthly_2022_10/Nova-Weather-zone-buffer-explanation.png.9ff2be4e8387080905e2a5850ca660da.png)](https://codefling.com/uploads/monthly_2022_10/Nova-Weather-zone-buffer-explanation.png.9ff2be4e8387080905e2a5850ca660da.png "Enlarge image")

    Climate definitions

This will contain the definitions for the climates to be used. Climate definitions are very straightforwards, we only need an enabled status and a list of assigned profiles.

    Climate definitions -> Enabled

This enables or disables a climate. A disabled climate will not do any calculations, or propagate any data to players. If you have a special event planned where you’d want to use a specific climate, but don’t want to accidentally use it elsewhere, you can disable it.

    Climate definitions -> Profiles

This is the list of assigned profiles. That’s it.

    Climate definitions -> Profiles -> Profile

The name of the profile to assign to this climate. Note that the name must match exactly, case sensitively.

    Climate definitions -> Profiles -> Chance

This is the chance (weight) for this profile. A climate will cycle through all profiles based on their weight; if one profile has a weigh of 1 and one has a weight of 10, the latter will be 10x more likely to be picked as the next profile to be loaded. The weight is not capped at 100, it is just named “chance” to make sure everyone understands its’ function.


## Configuration files: Profiles/*.json

With that out of the way, let’s dive into the profile configuration.

    {
        "Transition time (seconds)": 300,
        "Parent profile": "default_overcast",
        "Duration": {
            "Type": "range",
            "Min. seconds": 900,
            "Max. seconds": 1800
        },
        "Base properties": [
            {
                "Property": "wind",
                "Value": 0.8
            },
            {
                "Property": "rain",
                "Value": 1
            }
        ],
        "Steps": {
            "0": [
                {
                    "Type": "Property",
                    "Property": "cloud_coverage",
                    "Value": 0.8,
                    "Fade (seconds)": 60
                }
            ],
            "60": [
                {
                    "Type": "Property",
                    "Property": "cloud_attenuation",
                    "Value": 0.7,
                    "Fade (seconds)": 30
                }
            ]
        }
    }
This contains the following fields:

    Transition time (seconds)

Determines the duration of the transition between the last profile and this one. When a climate is cycling through the profile’s timeline and the timeline ends, the next profile will be loaded and the transition to it will start from the last frame of the last profile. If you set this to 0, the new profile just pops into existence. Set this to 10 and over 10 seconds the old profile vanishes and the new one appears.

    Parent profile

There’re about 20 weather settings to mess around with, so if you had to enter them all every time it’d be annoying as ****. Thats why we’ve implemented profile inheritance. If you leave this empty you need to enter all 20 properties yourself, but if you already have a profile with properties you like and wish to modify a bit, you can enter that there.

Say for example you have a “storm” profile with a regular old storm. But then, in addition to that regular storm, you also want a profile that storms but that also thunders and has a deep red sky. But you don’t want to have to copy-paste the “storm” profile.

Instead what you can do is set the parent profile to “storm”, and then just set the thunder property to 1 and the atmosphere rayleigh to whatever you want. The profile will then use the properties of “storm” as a base, and use its’ own base properties to override those. This way you can make infinite variations of similar weather types.

    Duration

Speaks for itself; the profile’s actual duration. There’re two types, “static” and “range”. If the type is set to “range”, it will randomly pick a number between the min and the max values. If the type is set to “static”, it will always pick the min. seconds value as its’ duration.

    Base properties

These are the profile’s properties that are always set and will be transitioned to when the profile loads. You can find all possible properties in the “detailed convars” section of the following URL:  [https://wiki.facepunch.com/rust/Weather#detailedconvars](https://wiki.facepunch.com/rust/Weather#detailedconvars)

In the profile’s properties you don’t include the “weather.” prefix for those properties, so “weather.rain” just becomes “rain”.

The only property not included in that list that is usable with Nova Weather is the “temperature” property. This property is used to override the locally calculated temperature (think of temperature drops at night and such) and will always be the temperature you enter. This property can also be animated with steps.

    Steps

This is how you animate a weather profile. Using steps, you can populate the profile’s timeline however you see fit. Remember that fun timeline graphic at the top of the page?
![Timelines](https://hypernova.gg/vendor-products/harmony/novaweather/timeline.png)

That roughly translates to:

    "Steps": {
        "5": [
            {
                "Type": "Property",
                "Property": "cloud_coverage",
                "Value": 0.8,
                "Fade (seconds)": 120
            }
        ],
        "30": [
            {
                "Type": "Property",
                "Property": "rain",
                "Value": 1.0,
                "Fade (seconds)": 120
            }
        ],
        "130": [
            {
                "Type": "Property",
                "Property": "thunder",
                "Value": 1.0,
                "Fade (seconds)": 150
            }
        ]
    }

Steps are put at static positions in the timeline by setting it to a specific second. Want rain to come in at the 30 seconds mark? You add a step at “30”.

A step is animated as well; you can have the rain come in at 30 seconds and have it take 60 seconds to go from just a drop to a full on downpour. It’s all in the fade time.

Within a step there’s four properties:

- **Type** – this is either “Property” (case sensitive!) or “Command”.

- **Property** – this is the actual weather property name like “wind” or “rain” and such

- **Value** – the value of that property, usually between 0 and 1

- **Fade (seconds)** – the amount of time it should transition from base value to the new value


# Extras
Nova Weather will release with a few very basic weather profiles that showcase the function of the mod with base properties and timeline steps. You can play with this to your heart’s content.

But, for those of you who are not super keen on spending hours configuring the perfect weather, we’re way ahead of you.

Our team is working on a set of beautiful weather profiles that’ll be released on all marketplaces in the near future. This takes significant amounts of time, so it may not yet be released at the time you’re reading this. But if they are, they will be released either for free or for a small fee. Important to note is that any profile packs that you purchase from us are licensed, and therefore cannot be shared with others who have not bought the pack.

# FAQ

> **Question:**  How do I share profiles?

Profiles are separate files that are found in the /Profiles folder of the Nova Weather folder. These profiles are in .json format and can be shared basically anywhere. All you have to do to import them is to place the .json file you received into your /Profiles folder with the other profile files, and reload the mod using the appropriate command.

> **Question:** The transitions are super stuttery, can I make them smoother?

The smoothness of the transitions is determined by your Tickrate setting. If you set this to 10, then the mod will calculate new values every 10th frame. To make transitions smoother, you lower the Tickrate setting by either modifying the Configuration.json or use the appropriate command. Note that if you lower this number, the load on your server will slightly increase due to it having to calculate more often.
