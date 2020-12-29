# i3-QuakeTerm

A quake-like drop-down terminal for i3.
Each call to the i3-quaketerm command will either:
  * Create a terminal and show it at the top or bottom of the focused workspace.
  * Bring back the terminal to the focused workspace if hidden or on other workspace.
  * Hide the terminal into scratch pad if already visible on focused workspace.

This was inspired by a similar drop-down terminal for AwesomeWM and [i3-quickterm](http://github.com/lbonn/i3-quickterm)
another similar drop-down terminal for i3. Initially a workaround for a bug in i3ipc-python, the differences with the
former are the following:

  * No configuration file (everything can be done from the command line).
  * Uses WM_CLASS instance attribute instead of i3's mark to identify the terminal.
  * Fork terminal instead of in-place creation.

## Usage

After you have installed the script, you may bind it to a key inside i3.
This will toggle the drop-down terminal or create it when needed.
It is also recommended to pre-float the terminal window in i3 to avoid
influence on other container when the terminal is created.

```
for_window [instance="i3-quaketerm"] border none floating enable
bindsym F12 exec i3-quaketerm
```

The initial terminal creation might take some time. It is possible
to create this terminal when i3 starts instead by using the `-H, --hidden`
option. This will hide the terminal when it is first created.

```
exec i3-quaketerm -H
```

Finally, it is possible to integrate the drop-down terminal with other tools.
For example, transparency with compton compositor (in `compton.conf`).

```
opacity-rule = [ "95:class_g='i3-quaketerm'" ];
```

## Other commands than just shell

It is also possible to add extra options to the terminal and to map alternative
drop-down terminals to different keys using the `-e, --extra-options` and
`-n, --name` options. For instance, you can change the terminal color, run Haskell
interpreter, Python or anything you like. We use `-n, --name` to distinguish
between the different instance of the drop-down terminal.

```
bindsym F12 exec i3-quaketerm -e "-rv"
bindsym F11 exec i3-quaketerm -n i3-haskell-quaketerm -e "ghci"
bindsym F10 exec i3-quaketerm -n i3-python-quaketerm -e "bpython"
```

## Other terminals than just XTerm

By default, the command will use XTerm, but you can of course use another terminal
with the `-t, --terminal` option. The terminal must support the equivalent of the
`-name` option of XTerm. This changes the application name, so it can be identified
among all others windows within your window manager. If the terminal does not use
`-name`, we can specify the correct option to use with `-N, --name-option`.

```
i3-quaketerm -t sakura -N --name
```

## Side panels

Instead of a dropdown terminal, you can also use this command to pop-up side panels
with the `-a, --align` option. This can be useful when the drop-down terminal not
tall enough for some tasks, such as reading man pages or quickly editing files.

```
i3-quaketerm -n i3-right-term -a right --height 1.0 --width 0.45
i3-quaketerm -n i3-left-term -a left --height 1.0 --width 0.45
```

## One instance per workspace

It is possible to create one instance of terminal per workspace instead of one common
to all workspaces. To do so, use the `-W, --workspace` option. This will append
`:{workspace-id}` to the instance name where `{workspace-id}` is either the logical
number or if not available, the name of the currently focused workspace. Thus,
it will automatically create a distinct instance name for each workspace. For example,
the following i3 binding will create one drop-down terminal for each of your workspace,
always accessible through the same key.

```
bindsym F12 exec i3-quaketerm -W
```

## Other cool ideas

If you have any other cool idea about how to use this command, specific configuration
for your own setup, own terminal, bug reports or any other improvement, feel free to
send them as [issues](https://github.com/gawen947/i3-quaketerm/issues) or
[pull requests](https://github.com/gawen947/pulls).
