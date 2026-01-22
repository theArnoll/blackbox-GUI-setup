# General Setup:

Run `setup.sh`

It will install:
- Brave Browser
- VSCode
- scrcpy
- syncthing
- neofetch
- zsh

Username: blackbox

The device I'm buying is likely 天虹 QN10 (China CCC no. 2020010901352389)  
[Unbox YouTube video from others (zhTW)](https://youtu.be/yfO0vQPTrPM)  
[Unbox paragraph (zhCN)](https://post.smzdm.com/p/akk9g20k/)  
May not come with SATA FPC cable

# Resolve Logitech K400r touchpad scrolling issue

1. Find K400r
```bash
xinput list
```

Check if the keyboard called `Logitech K400r` or `Logitech Unifying Device. Wireless PID:xxxx` or something else

2. Create configuration file
```bash
sudo nano /usr/share/X11/xorg.conf.d/99-k400r-scrolling.conf
```

3. Paste this
It means "if the device name contains 'K400' and is a pointer device, enable natural scrolling".
```conf
Section "InputClass"
    Identifier "Logitech K400r Natural Scrolling"
    MatchDriver "libinput"
    MatchProduct "K400"  # Fill the item you found in "xinput list"
    Option "NaturalScrolling" "true"
EndSection
```

* You can also use this:
```bash
sudo cat <<EOF > /usr/share/X11/xorg.conf.d/99-k400r-scrolling.conf
Section "InputClass"
    Identifier "Logitech K400r Natural Scrolling"
    MatchDriver "libinput"
    MatchProduct "K400"  # Fill the item you found in "xinput list"
    Option "NaturalScrolling" "true"
EndSection
EOF
```
! Remember editing MatchProduct to match your device name! (You can chose to use "K400" or "Wireless PID:xxxx")

4. Make it happen
Login and reboot, your K400r will have natural scrolling, while other brand mice plugged in will remain the same.
