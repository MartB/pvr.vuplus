[![Build Status](https://travis-ci.org/kodi-pvr/pvr.vuplus.svg?branch=master)](https://travis-ci.org/kodi-pvr/pvr.vuplus)
[![Coverity Scan Build Status](https://scan.coverity.com/projects/5120/badge.svg)](https://scan.coverity.com/projects/5120)

# VuPlus PVR
VuPlus PVR client addon for [Kodi] (http://kodi.tv)

## Build instructions

### Linux

1. `git clone https://github.com/xbmc/xbmc.git`
2. `git clone https://github.com/kodi-pvr/pvr.vuplus.git`
3. `cd pvr.vuplus && mkdir build && cd build`
4. `cmake -DADDONS_TO_BUILD=pvr.vuplus -DADDON_SRC_PREFIX=../.. -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX=../../xbmc/addons -DPACKAGE_ZIP=1 ../../xbmc/cmake/addons`
5. `make`

##### Useful links

* [Kodi's PVR user support] (http://forum.kodi.tv/forumdisplay.php?fid=167)
* [Kodi's PVR development support] (http://forum.kodi.tv/forumdisplay.php?fid=136)

## Configuring the addon

### General
Within this tab the mandatory addon options need to be configured before it can be successfully enabled.

* **VU+ hostname or IP address**: The IP address or hostname of your enigma2 based settop box.
* **Fetch picons from web interface**: Fetch the picons straight from the Vuplus/Enigma 2 STB
* **Use picons.eu file formate**: Assume all picons files fetched from the STB start with `1_1_1_` and end with `_0_0_0`
* **Icon Path**: In order to have Kodi display channel logos you have to copy the picons from your settop box onto your OpenELEC machine. You then need to specify this path in this property.
* **Update Interval in minutes**: As the settop box can also be used to modify timers, delete recordings etc. and the settop box does not notify the Kodi installation, the addon needs to regularly check for updates (new channels, new/changed/deletes timers, deleted recordings, etc.) This property defines how often the addon checks for updates.

### Channels & EPG
Within this tab options that refer to channel and EPG data can be set.

* **Fetch only one TV bouquet**: If this option is set than only the channels that are in one specified TV bouquet will be loaded, instead of fetching all available channels in all available bouquets.
* **TV-Bouquet**: If the previous option has been enabled you need to specify the TV bouquet to be fetched from the settop box. Please not that this is the bouquet-name as shown on the settop box (i.e. "Favourites (TV)"). This setting is case-sensitive.
* **Zap before channelswitch (i.e. for Single Tuner boxes)**: When using the addon with a single tuner box it may be necessary that the addon needs to be able to zap to another channel on the settop box. If this option is enabled each channel switch in Kodi will also result in a channel switch on the settop box. Please note that "allow channel switching" needs to be enabled in the webinterface on the settop box.
* **Extract Genre, Season and Episode Info where possible**: Have kodi check the description fields in the EPG data and attempt to extract genre, season and episode info where possible.

### Recordings & Timers

* **Recording folder on receiver**: Per default the addon does not specify the recording folder in newly created timers, so the default set in the settop box will be used. If you want to specify a different folder (i.e. because you want all recordings scheduled via Kodi to be stored in a separate folder), then you need to set this option.
* **Use only the DVB boxes' current recording path**: If this option is not set the addon will fetch all available recordings from all configured paths from the STB. If this option is set then it will only list recordings that are stored within the "current recording path" on the settop box.
* **Keep folder structure for records**: If enabled do not specify a recording folder, when disabled (defaut), check if the recording is in it's own folder or in the root of ht recording path
* **Enable generate repeat timers**: Repeat timers will display as timer rules. Enabling this will make Kodi generate regular timers to match the repeat timer rules so the UI can show what's scheduled and currently recording for each repeat timer.
* **Number of repeat timers to generate**: The number of Kodi PVR timers to generate.
* **Enable AutoTimers**: When this is enabled there are some settings required on the STB to enable linking of AutoTimers (Timer Rules) to Timers in the Kodi UI. On the STB enable the following options (note that this feature supports OpenWebIf 1.3.x and higher):
  1. Hit `Menu` on the remote and go to `Timers->AutoTimers`
  2. Hit `Menu` again and then select `6 Setup`s
  3. Set the following to option to `yes`
    * `Include "AutoTimer" in tags`
    * `Include AutoTimer name in tags`
* **Automatic Timerlist Cleanup**: If this option is set then the addon will send the command to delete completed timers from the STB after each update interval.

### Timeshift
* **Enable Timeshift**: What timeshift option do you want. `Disabled`, only timeshift `On pause` or timeshift `On Playback`.
* **Timeshift buffer path**: The path used to store the timeshoft buffer. The default is the addon data folder in userdata

### Advanced
Within this tab more uncommon and advanced options can be configured.

* **Enable automatic configuration for live streams**: When enabled the stream URL will be read from an M3U file. When disabled it is constructed based on the filename.
* **Streaming Port**: This option defines the streaming port the settop box uses to stream live tv. The default is 8001 which should be fine if the user did not define a custom port within the webinterface.
Webinterface Port: This option defines the port that should be used to access the webinterface of the settop box.
* **Username**: If the webinterface of the settop box is protected with a username / password combination this needs to be set in this option.
* **Password**: If the webinterface of the settop box is protected with a username / password combination this needs to be set in this option.
* **Send DeepStandby-Command**: If this option is set then the addon will send the DeepStandby-Command to the settop box when Kodi will be closed (or the addon will be deactivated), causing the settop box to shutdown into DeepStandby.
* **Custom Live TV timeout (0 to use default)**: The timemout to use when trying to read live streams