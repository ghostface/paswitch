# paswitch

CLI application to switch between PulseAudio sinks, as defined by the user with a friendly name.

# Changes in this fork

- Use pactl instead of pacmd
- Works with pipewire
- Read the current default sink from pa/pipewire instead of the config file
- Relocate all sink inputs when switching and rename parmeter to --norelocate to disable
- Set target sink as default when switching and rename parameter to --keepdefault to not do this
- Added volume icon to notification display (audio-volume-high)

# Requirements

For this tool to function you must have the `pactl` program installed on your (Linux) machine.

Optionally, you need `libnotify` (`libnotify` on Pacman for example) if you want notifications.

# Installation

`npm install -g paswitch`

# Configuration

The first time paswitch is called, it will create a configuration file (under $HOME/.config/paswitch/) along with the command you enter.

Before you can begin, you need to add some sink data.

# Usage

## Add/set sink

Syntax: `paswitch set-sink <friendly-name> <sink-name>`

Where `<friendly-name>` is the shorthand name you want to give to the sink, and `<sink-name>` is the name of the sink as seen in the command `pactl list sinks | grep "Name:"`

## Remove sink

Syntax: `paswitch remove-sink <friendly-name>`

Where `<friendly-name>` is the shorthand name you have given the sink earlier.

This will forget the sink.

## Switch to a sink

Syntax: `paswitch switch <friendly-name>`

Where `<friendly-name>` is the shorthand name you have given the sink earlier.

This will switch to that sink as the default/unmuted one.

## Toggle sinks

Syntax: `paswitch toggle`

This will set the next sink in the list as the default/unmuted one.

## List sinks

Syntax: `paswitch list`

This will list all memorized sinks.

## Start a wizard

Syntax: `paswitch wizard <type>`

This will start a wizard of the selected type, to easily manage sinks.

## Options

```
-k, --keepdefault  -- Do not set the default sink to the target sink by making it the default sink
-m, --mute         -- Switches to the target sink by unmuting it and muting all other memorized sinks
-n, --norelocate   -- Do not relocate existing application sink inputs to the new sink
```

## Wizard types

```
add-sink           -- Shows an interactive list of connected sinks to select and add
remove-sink        -- Shows an interactive list of remembered sinks to forget
```

Note that you can combine `--nodefault`, `--norelocate` and `--mute` options.
