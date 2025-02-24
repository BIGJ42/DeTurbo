# turbo-boost-disable
This is an app that uses edupr91's script and the [Turbo Boost Switcher (TBS)](https://github.com/rugarciap/Turbo-Boost-Switcher) kext to disable turbo boost easily.

## Disclaimer
This tool is **only an app** to use [Turbo Boost Switcher (TBS)](https://github.com/rugarciap/Turbo-Boost-Switcher) in the background. 

This issue only affects Intel Macs.
If you're using an Apple Silicon based Mac, you are free from overheating by design!
Additionally, the kext shown here will only work on Intel-based Macs.

## Why?
My 2012 Intel MacBook Pro can get quite hot. 
It's well known that integrated circuits last longer if they are not stressed out as much during their life.
That means (relatively) cool operation most of the time.

I love TBS but was being constantly bombared with at least 3 login prompts every time I unlocked my computer.
There were no workarounds for this as far as I could tell, so I wrote an app to use edupr91's script to use the kext from [Turbo Boost Switcher (TBS)](https://github.com/rugarciap/Turbo-Boost-Switcher) to disable/enable Turbo Boost in an even easier way than his shell script [(here it is)](https://github.com/edupr91/turbo-boost-disable).

This program runs totally silently in the background and I never have to think about it; the same goes for my MacBook.
It's finally cool, calm, and lasts longer on battery life.

# Install

This is just an app to use a kext to disable Turbo Boost on 64-bit macOS, taken directly from [TBS](https://github.com/rugarciap/Turbo-Boost-Switcher).

We have to use the direct TBS kext because for some reason, their kext can run on macOS, but we cannot sign our own version to work on macOS. They must have signed it with an Apple key or something?
Anyway, to get around having to use the crappy Turbo-Boost Switcher GUI, we take the core kext, which is directly enabled/disabled with the app in this repo. Enjoy!

I have built a single app to run these scripts so the process can be setup easier.

## 1. Setup (Required)
1. Install [Turbo Boost Switcher](https://github.com/rugarciap/Turbo-Boost-Switcher)
2. Ensure the folder provided in TBS is called tbswitcher_resources and place it in the applications folder
3. Download the latest release and place the app in the applications folder.
4. We need to allow the app to run as root without the need for a password on every login
   Therefore, modify your `/etc/sudoers` file to not require a password for these scripts.
   Edit the sudoers file:
   ```sh
   $ sudo visudo /etc/sudoers
   ```

   Add these lines to `/etc/sudoers`, below
   ```
   root            ALL = (ALL) ALL
   %admin          ALL = (ALL) ALL
   ```
   replacing `USERNAME` with your login username (use `whoami` to find this out):
   ```
   USERNAME ALL=(ALL) NOPASSWD: /usr/bin/kextutil
   ```

   You can now choose automatic control or manual control to disable Turbo Boost.

## 2a. Automatic Control (suggested)
To ensure Turbo Boost is always disabled, we need to run the app every time the computer is unlocked.
This is because after unlock the kext will stop working (for some reason).
This can be easily done on MacOS.
1. Go to system settings.
2. Go to Login items.
3. Click the plus icon.
4. Select the app you just put in the applications folder.

This will be opened in the background each time the computer is unlocked, and works well (for me at least).

## 2b. Manual Control (if you want)
As long as you followed step (1) above, the app should not require a password to run.

Bear in mind that after enabling, it probably will auto-disable after the next computer unlock.
You should use the Automatic Control directions to ensure that Turbo Boost is always disabled.
To reenable turbo boost temporarily, use the Enabler App and to stop it disabling again, remove the Disabler from the login items. To re-disable Turbo Boost without logging out, Simply open the Disabler app.
## Licence
This software fundamentally relies on the TBS kernel extension (kext).
This repository is distributed under the GNU General Public Licence v2.0, of which the terms are:

```
Turbo Boost disabler / enable app for Mac OS X
Copyright (C) 2013  rugarciap

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License along
with this program; if not, write to the Free Software Foundation, Inc.,
51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.
```

In accordance with the terms of the licence, we are distibuting this software under the same licence.
We simply provide a non-GUI interface to interact with this kext.

Our licence:
```
Turbo Boost Disabler - An app to Disable Turbo Boost on Intel Macs.
Copyright (C) 2025 BIGJ

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License along
with this program; if not, write to the Free Software Foundation, Inc.,
51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.
```
