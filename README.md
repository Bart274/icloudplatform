# icloudplatform
This will be the repo where I'll work on my new implementation of the icloud platform for home-assistant

# Installation steps:
- Download icloud.py from this repo and put it in .homeassistant\custom_components
- Remove icloud config from the `device_tracker:` config
- Stop HA
- Run `pip install pyicloud` in the environment where HA is running
- Add `icloud:` config to your HA config, see the config.txt file for an example.
- Start HA

# Config options:
- `ignored_devices` contains a list of all devices linked to your account that you don't want to track
- `manual_update` is a list of fixed times on which your devices will be updated, no matter what the interval is at that point
- `googletraveltime` contains a dict of idevices that are linked to a sensor which state is in minutes (like the Google Maps Travel Time Sensor). This sensor will be used to calculate the interval when the distance from home is greater than 100km.
- `events` if this is `True`, the events from you icloud calendar will be shown in the UI. The icloud entity will gain 2 additional attributes, one that shows how many current events are happening and one that shows how many upcoming events you have in the next 7 days.

# Family sharing:
There are some users reporting that if they have family sharing enabled, only the devices of one account are being updated.
To resolve this, I suggest you add all the accounts to your `icloud:` config, but put all the devices that aren't linked to that account in it's `ignored_devices` list.
For example:
```
icloud:
  person1:
    username: ***
    password: ***
    ignored_devices:
      - <iphone of person2>
  person1:
    username: ***
    password: ***
    ignored_devices:
      - <iphone of person1>
```