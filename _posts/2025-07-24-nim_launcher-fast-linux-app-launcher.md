---
title: "nim_launcher — A Fast and Minimal Linux App Launcher in Nim"
date: 2025-07-24
tags: [nim, linux, x11, rofi-alternative, launcher, wayland, xwayland]
categories: [projects, linux, development]
layout: post
toc: true
comments: true
---

![nim_launcher Screenshot](/assets/images/nim_launcher_dracula.png)

`nim_launcher` is a lightweight and fast application launcher for Linux, written entirely in [Nim](https://nim-lang.org/).  
I built this mostly for myself because I wanted something minimal like [Rofi](https://github.com/davatorium/rofi), but more hackable and easier to maintain — no GTK, no Qt, just a raw X11 interface and some simple fuzzy logic.

It runs on X11, and by extension, works fine under Wayland via XWayland.

## Why Write My Own Launcher?

Rofi is great — but over time I found it increasingly heavy for what I actually use it for:  
- launching apps  
- not styling widgets  
- not scripting multi-step menus  

I wanted something that:
- launches instantly  
- doesn't require a pile of dependencies  
- I can configure in an INI file without reading a man page  
- just works with X11 (and optionally XWayland)

So, I wrote one.

## Key Features

- Fuzzy Search: instant filtering of apps as you type  
- Keyboard Driven: arrow keys, Enter to launch, Esc to cancel  
- Centered, Borderless Window: like Rofi, but cleaner and faster  
- Fast Startup: smart caching avoids repeated scans  
- Fully Configurable: editable `config.ini` for tweaking layout, colors, prompt  
- No GTK/Qt: just direct X11 bindings in Nim (via `x11` Nim module)

## How to Build It

You’ll need:
- Nim installed ([instructions here](https://nim-lang.org/install.html))  
- X11 dev libraries

Then:

```bash
git clone <your-repo-url>
cd nim_launcher
nimble install x11
nim compile -d:release src/nim_launcher.nim
```

It’ll produce an executable you can move somewhere like `~/.local/bin`.

## Usage

Once installed, bind a hotkey in your window manager.  
For i3 users, something like this:

```
bindsym $mod+d exec ~/.local/bin/nim_launcher
```

You can now hit `Mod+D` and get a centered, fuzzy-searchable app launcher — no fuss.

## Configuration

When first run, `nim_launcher` generates a config file at:

```
~/.config/nim_launcher/config.ini
```

Everything from colors to layout can be tweaked there. A few highlights:

```ini
[window]
width = 600
center = true
max_visible_items = 10

[colors]
background = "#2E3440"
foreground = "#D8DEE9"
highlight_background = "#88C0D0"

[input]
prompt = "> "
cursor = "_"
```

## Roadmap

I’ve marked the core feature set as “done”, but I do have a few stretch goals:

- TTF/Font rendering via `Xft`
- Icon support for applications
- More advanced fuzzy logic (Levenshtein?)

## Final Thoughts

This started as a side-project and quickly became a daily driver.  
If you’re on a tiling WM and want a super fast launcher without a pile of dependencies — give it a go.

Code’s on GitHub/GitLab/etc. under GPLv3. Suggestions, forks, and pull requests are always welcome.

> [cheesydoodle.com](https://www.cheesydoodle.com) — Craig
