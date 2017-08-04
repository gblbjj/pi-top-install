# pi-top-install
Do you want to run the standard **raspbian jessie** on the pi-top or pi-topCEED?
In this repository you find tips, tricks and scripts to install the necessary capabilities to control
the pi-top hardware using a standard raspbian jessie distribution.

For other linux distributions, see the links at the bottom of this page.

**1 - Battery status display widget (released)**

See separate repository https://github.com/rricharz/pi-top-battery-status

This program has been tested on raspbian jessie and pi-topOS and should work well with any
distribution. Do not forget to turn **i2c** on in *Menu/Preferences/Raspberry Pi Configuration/Interfaces*.
The program will display the battery status, 
and will shut down the Raspberry Pi if the battery capacity is low and not
charging. But unless you also install 3 (automatic poweroff) it will not be able
to turn off the pi-top hub and the power to the Raspberry Pi. It would therefore
not protect the battery from further depleting.

**2 - program to set the screen brightness (version 1.1, released)**

This program is for Raspbian Jessie only, it should not be installed in pi-topOS.

For installation instructions, see below under INSTALLATION INSTRUCTIONS FOR 2 AND/OR 3.

Usage (new_value is a screen brightness value between 3 and 10):
```
brightness new_value
brightness increase
brightness decrease
```

The keyboard brightness keys will work, if you put the following into the
keyboard section of /home/pi/.config/openbox/lxde-pi-rc.xml:
```
    <keybind key="0xC7">
      <action name="Execute">
        <command>brightness increase</command>
      </action>
    </keybind>
    <keybind key="0xC6">
      <action name="Execute">
        <command>brightness decrease</command>
      </action>
    </keybind>
```

Instead, you can also copy the lxde-pi-rc.xml file found in this repository to /home/pi/.config/openbox
This filealso contains working keys for autio mute toggle, audio volume +, audio volume -, file manager and terminal.

Very experienced users can use the command "brightness off" to turn the screen backlight off, and "brightness on"
or any other brightness command to turn it back on. But be aware that a turned off screen backlight might easily be
mistaken for a Raspberry Pi, which has been shut down. Do not shut off your rpi or cut power to it in this state,
and do not use "brightness off" unless you have tested that your brightness keys work, so that you can turn power
back on! Also, please be aware that if you have a laptop pi-top with battery, it still draws power from the battery
in this state. In order to save battery power, it is much better to shut down the pi-top as you would
normally do. It is therefore not recommended for regular users to use the command "brightness off"! 


**3 - program and system service to turn the hub-controller off after shutdown (version 1.1, released)**

This program is for Raspbian Jessie only, it should not be installed in pi-topOS.

This program will help to protect your battery by shutting the pi-top-hub-controller
off after a shutdown of the Raspbery Pi

**INSTALLATION INSTRUCTIONS FOR 2 AND/OR 3**

To download this repository, open a terminal and type:
```
sudo apt install wiringpi
cd Downloads
git clone --depth 1 git://github.com/rricharz/pi-top-install
cd pi-top-install
chmod +x install*
```

Make sure that **spi** is turned on in *Menu->Preferences->Raspberry Pi Configuration->Interfaces*.

Make sure that your system is up-to-date:
```
sudo apt update
sudo apt upgrade
```

To install 2 (brightness):
```
./install-brightness
```

To install 3 (automatic poweroff)
```
./install-poweroff
```

Your new software will work after the next bootup.

*Instructions to compile the programs*

To compile the  programs (only required if you want to modify the c programs), use
```
make
```
Then use the install scripts again to reinstall the programs

*Upgrading the programs*

Open a terminal and type

```
  cd Dowloads/pi-top-install
  git pull
  install-brightness
  install-poweroff
```

If you do not have the folder pi-top-install in Downloads anymore, you need to do a complete new installation.

*What to do if brightness and shutdown stop working*

If you have just upgraded your system and brightness or shutdown does not work anymore, install the programs again.
Something might have been overwritten during the upgrade process.

Is is possible to put the pi-top-hub-controller into a strange state by experimenting with other devices on the
spi bus. In this state it will not accept commands anymore. For details see the closed issue #2
"Brightness not working - pi hub in strange state?" in this repository, which also contains the information needed
to resolve this problem.

**4 - Use the pi-top speaker with Raspbian Jessie (and pi-topOS)**

Pi-top has added instructions for the installation of the pi-top-speaker in Raspbian Jessie at
https://github.com/pi-top/pi-topSPEAKER.

**Feedback**

Please open an issue in this repository to report problems.

The contributions in this repository are distributed in the hope that they will be useful, but WITHOUT ANY WARRANTY;
without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. The owner of this repository
is not affiliated with pi-top.

Using the pi-top with other linux distributions:
  - for a very nice bootable **64-bit Gentoo image for the Pi-Top**, see https://github.com/sakaki-/gentoo-on-rpi3-64bit
