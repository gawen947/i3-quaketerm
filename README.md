# i3-QuakeTerm

A quake-like drop-down terminal for i3.
Each call to the i3-quaketerm command will either:
  * Create a terminal and show it at the top or bottom of the focused workspace.
  * Bring back the terminal to the focused workspace if hidden or on other workspace.
  * Hide the terminal into scratchpad if already visible on focused workspace.

This was inspired by a similar drop-down terminal for AwesomeWM and [i3-quickterm](http://github.com/lbonn/i3-quickterm)
another similar drop-down terminal for i3. Initially a workaround for a bug in i3ipc-python, the differences with the
former are the following:

  * No configuration file (everything can be done from the command line).
  * Uses WM_CLASS instance attribute instead of i3's mark to identify the terminal.
  * Fork terminal instead of in-place creation.

Usage
-----

After you have installed the script, you may bind it to a key inside i3.
This will toggle the drop-down terminal or create it when needed.
It is also recommended to pre-float the terminal window in i3 to avoid
influence on other container when the terminal is created.

```
for_window [instance="i3-quaketerm"] floating enable
bindsym F12 exec i3-quaketerm
```

You can of course use another terminal with the `-t, --terminal` option.

```
bindsym F12 exec i3-quaketerm -t mlterm
```

The initial terminal creation might take some time. It is possible
to create this terminal when i3 starts instead by using the `-H, --hidden`
option. This will hide the terminal when it is first created.

```
exec i3-quaketerm -H
```

It is also possible to add extra options to the terminal and to map alternative
drop-down terminals to different keys using the `-e, --extra-options` and
`-n, --name` options.

```
bindsym F12 exec i3-quaketerm -e "-rv"
bindsym F11 exec i3-quaketerm -n i3-haskell-quaketerm -e "ghci"
bindsym F10 exec i3-quaketerm -n i3-python-quaketerm -e "bpython"
```

Finally it is possible to integrate the drop-down terminal with other tools.
For example, transparency with compton compositor (in `compton.conf`).

```
opacity-rule = [ "95:class_g='i3-quaketerm'" ];
```
