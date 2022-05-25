---
tags: scripts howto
author: oo
---

# Selecting Bose headset audio profile

Bose QuietComfort is a great headset. But switching between the high
fidelity and headset audio profiles in Linux normally requires going
into Settings or pauvcontrol and clicking about. So I made this script
based on
[this post](https://forums.linuxmint.com/viewtopic.php?t=295859). Set
it up as a keyboard shortcut in your window manager or something.

Download it [here](/scripts/bose) or cut and paste:

```

#!/bin/bash

# This will only work if you have just one card.
# This is a hack, not actually production code, d'uh
BOSE=$(pacmd list-cards | grep bluez_card | sed 's/.*<bluez_card.\(.*\)>/\1/')

case "$1" in
    audio)
	SINK=a2dp_sink
	;;
    mic)
	SINK=handsfree_head_unit
	;;
esac

pactl set-card-profile bluez_card.${BOSE} ${SINK}
pacmd set-default-sink bluez_sink.${BOSE}.${SINK}

```
