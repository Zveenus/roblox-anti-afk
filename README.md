# Roblox Anti-AFK

A small Windows tool that keeps you from getting AFK-kicked in Roblox, even while you're alt-tabbed into YouTube or whatever else.

Every few minutes it briefly brings Roblox to the front, taps a random set of movement keys, then puts you straight back where you were.

## Features

- Configurable interval, 0.5 to 15 minutes (default: 5)
- Random key combos each run (A+D, W+S, A+D+Space, etc.). Opposing keys cancel out, so your character jumps and twitches but doesn't walk off
- Randomized key order, hold times and gaps, plus optional timing jitter
- Works while you're in another window: it focuses Roblox, does its thing, then returns you to your previous window
- Handles minimized Roblox windows: restores it, sends the keys, minimizes it again
- Keys are sent as hardware scan codes, which Roblox actually registers
- "Test now" button to verify it works without waiting
- Dark UI with a live countdown and progress bar
- Zero dependencies, standard library only

## Download

Grab `AFK.exe` from this repo and run it. No install needed.

Or run from source:

```
python source.py
```

Requires Windows and Python 3.8+. No pip packages.

## Usage

1. Launch Roblox and join a game
2. Open the tool and set your interval
3. Hit **Start**
4. Use your PC normally. Every cycle, Roblox flashes up for about 3-4 seconds and you get returned to what you were doing

Use **Test now** once to confirm it finds your Roblox window.

Roblox kicks after 20 minutes of no input, so the 15 minute cap leaves a safe margin. 5 minutes is plenty.

## Why does it ask for admin?

To avoid interference. If Roblox or a game runs elevated, Windows blocks input and focus changes from non-elevated programs, so the tool would silently do nothing. Running as admin makes sure it always works.

## Can I trust it?

- The full source is right here: `source.py`. One file, short enough to read in a few minutes
- It makes no network connections, writes no files, and only reads window titles and class names to find Roblox
- You can scan `AFK.exe` with VirusTotal or any scanner you like. PyInstaller-built executables are sometimes flagged as false positives by a few engines, which is a known quirk of the packager and not specific to this tool
- Still don't trust the exe? Build it yourself (below)

## Build it yourself

With [auto-py-to-exe](https://pypi.org/project/auto-py-to-exe/):

- Script: `source.py`
- Onefile: One File
- Console: Window Based (hide the console)
- Advanced: enable "Request Administrator Privileges" (`--uac-admin`)

Or with PyInstaller directly:

```
pyinstaller --onefile --noconsole --uac-admin source.py
```

## Notes

- Windows only
- The PC must be awake and unlocked for window focusing to work
- If Roblox isn't running, the tool shows "Roblox not found" and tries again next cycle
- Use at your own risk. Automating input may go against the rules of some games, so check before using it anywhere it matters
