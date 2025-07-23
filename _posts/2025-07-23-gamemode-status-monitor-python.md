---
layout: post
canonical_url: https://www.cheesydoodle.com
toc: true
title: "[Doc] Monitoring Linux GameMode with Python and GTK Notifications"
date: 2025-07-23
categories: [Blog, Posts]
tags: ["Python", "GTK", "GameMode", "Linux", "Performance"]
excerpt: "A lightweight Python script that keeps an eye on Feral Interactive’s GameMode and pops up a desktop notification the moment the performance profile flips on or off."
---

![GameMode notification example](/assets/images/GameMode.Status.png)

If you run games on Linux, you’ve probably heard of **GameMode**.  
Flip it on and the daemon tweaks the CPU governor, I/O priorities, and a few other knobs so your frame‑times behave.  
Trouble is, there isn’t always a clear sign that the service actually kicked in when a game launches with the `gamemoderun` wrapper.

I threw together the small Python script below to solve that uncertainty.  
It polls `gamemoded -s`, shows a GTK desktop notification whenever the state flips, then steps out of the way.

## The Script

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
import os
import subprocess
from threading import Thread
from time import sleep
import gi
gi.require_version('Notify', '0.7')
from gi.repository import Notify

class GameModeStatusLoop(Thread):
    def __init__(self, interval):
        super().__init__(daemon=True)
        self.interval = interval
        self.status = "gamemode is inactive"
        self.start()

    def run(self):
        while True:
            currentstatus = self.GameModeStatus()
            if currentstatus != self.status:
                self.SendNotification("<b>GameMode</b>",
                                      f"<i>{currentstatus}</i>",
                                      "input-gaming")
                self.status = currentstatus
            sleep(self.interval)

    def GameModeStatus(self):
        result = subprocess.run(["gamemoded", "-s"], stdout=subprocess.PIPE)
        return result.stdout.decode().strip()

    def SendNotification(self, title, message, icon):
        if Notify.init("GameModeStatus"):
            Notify.Notification.new(title, message, icon).show()
            Notify.uninit()

def IsPackageInstalled(pkgname, pkglocation="/usr/bin"):
    return any(p.lower().startswith(pkgname.lower())
               for p in os.listdir(pkglocation))

if __name__ == "__main__":
    if IsPackageInstalled("gamemode"):
        GameModeStatusLoop(2)
        while True:
            sleep(1)
    else:
        print("gamemode package not found; please install it first.")
```

## How It Works

The heart of the script is the `GameModeStatusLoop` thread.  
Every _n_ seconds (two, by default) it asks the daemon for its current status.  
When the string returned by `gamemoded -s` changes, a desktop notification appears using **libnotify**.  
Because the thread is marked _daemon_, it exits cleanly when you close the parent process — no orphaned loops.

Before any of that, the helper `IsPackageInstalled` does a quick directory listing of `/usr/bin` to make sure the `gamemode` binaries exist.  
It’s a blunt check but it avoids spawning a subprocess if the package is missing.

## Why Not Just Watch Logs?

You can tail `journalctl -fu gamemoded` if you want, but that’s another window to juggle.  
A toast in the corner of the screen is harder to miss, and you don’t have to alt‑tab out of the game to verify it.

## Tweaks You Might Want

Change the poll interval if two seconds is too chatty, swap the icon name to match your GTK theme, or send the status to a system tray applet instead of a transient notification.  
The core loop stays the same.

## Closing Thoughts

GameMode is one of those set‑and‑forget tools — right up until you forget whether it’s actually set.  
This script gives an immediate, visual confirmation, no clutter, and minimal overhead.  
Drop it into your autostart and you’ll always know when the performance profile is active.

You’ll find the latest version in my gitlab repository’s, but the snippet here is enough to run as‑is.  
Feel free to adapt it, and if you add a neat feature, send a patch my way.
If you're interested in more code like this, feel free to explore the rest of the blog at [cheesydoodle.com](https://www.cheesydoodle.com).
