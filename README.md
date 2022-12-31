![GitHub ReadMe Banner](https://user-images.githubusercontent.com/58088168/210141506-722f4395-a598-4cf1-ba64-0caba1c09171.jpg)

# Welcome to the Hyperpixel 4 & Raspberry Pi Mount for Voron 2.4 GitHub Repo

###### A quick disclaimer
*Please note that Print Up is not affiliated with Voron or the Voron Design Team. We are simply fans of the Voron printers and want to contribute to the open-source community by providing helpful resources and support for these amazing machines.*

## About the Hyperpixel 4 Mount

The Hyperpixel 4 Mount for Voron 2.4 is a full solution for mounting the Hyperpixel 4 display by Pimoroni attached to a Raspberry Pi 3/4 via GPIO to a Voron 2.4 3D printer. This requires fully replacing the front skirt to your Voron 2.4 with a new bespoke solution that allows the almost vertical mounting of the Raspberry Pi directly behind the Hyperpixel Display.

The solution includes several 3D printable parts, a full visual manual, Hyperpixel configuration for Klipper Screen and more.

<img width="2053" alt="Example Image - CAD" src="https://user-images.githubusercontent.com/58088168/210150665-1d2ba202-fe59-42b3-9007-f21a1bc74fc6.png">

## What's included in the repo?
- **STL files** - All the printed parts
- **STEP file** - Should you wish to modify or create your own variant
- **Install Manual** - For the printed parts
- **Hyperpixel Config Guide** - for Klipper Screen
- **Example Images** - So you know what it looks like!

# Install Manual

The install manual will guide you through the physical part installation of the project. The Hyperpixel configuration can be found in this ReadMe. 

# Bill Of Materials (BOM)

For this project you will require the following items:
- 1x Hyperpixel 4 Display Rectangular by Pimoroni
- 1x Raspberry Pi 4 or 3B
- All the printed parts required for your printer (full details in the manual)
- 16x M3 x 8mm SHCS (Socket Head Cap Screw)
- 4x M2.5 x 6mm BHCS <sup>(1)</sup>
- 4x M2.5 x 15mm Standoffs <sup>(1)</sup>
- 12 x M3 x 5.7mm Heat Set Insert - We recommend the ones from CNC Kitchen or their resellers.
- Front Left & Right Belt Guards from the original Voron 2.4 printed parts. 
- Right Angle USB-C connector (for RPi 4) or Right Angle USB Micro B connector (for RPi 3B) <sup>(2)</sup>

*(1) These might be included with your Hyperpixel 4.*

*(2) You can install this without a Right Angle USB connecter however, we still recommend one to avoid bending the cable.*

## Tools

- An M3 Hex Allen Key or Screwdriver with a Hex M3 bit - You may benefit from an Allen Key that can be used at an angle such as the Wera Hex Keys with a Ball-End. 
- The mounting system kit, including all necessary screws and brackets - You can find the full BOM (Bill of materials in the manual or on GitHub (This is just above here))
- A soldering iron (ideally with a tip for M3 heat-set inserts, although a normal tip will work)
- A Voron 2.4 printer

# Hyperpixel Raspberry Pi Configuration

**Using Raspberry Pi OS Bullseye?**

Support for the Hyperpixel is built right into the OS, so no need to download anything! We just need to make some changes to the `/boot/config.txt` file as well as create a new configuration for the screen rotation. 

**Not using Raspberry Pi OS Bullseye?**

If you're not using OS Bullseye then you will need to install the Hyperpixel using the instructions from Pimoroni. https://github.com/pimoroni/hyperpixel4

## Configuration 💻 ⬇️

> ❗️ Not installed the printed parts yet? We recommend installing those first, however, you can follow the configuration first if you want to test the screen before installing. 

> ❗️ Please note, this config method might not work for OS versions before Bullseye, but if it does, please let us know!

**1. Install Klipper Screen**

- If you haven't already, install Klipper Screen. We recommend following the Manual Install Guide here - https://klipperscreen.readthedocs.io/en/latest/Installation/#auto-install

**2. SSH into your Raspberry Pi**

- SSH into your Raspberry Pi using Terminal (macOS/Linux) or PuTTY for Windows Users. In the example below just swap `yourpiaddress` for your Raspberry Pi's IP address or `yourpisname.local`

```
ssh pi@yourpiaddress
```

**3. Navigate to `/boot/config.txt` file**

- Using the following command, navigate to the `/boot/config.txt` file. 

```
sudo nano /boot/config.txt
``` 

**4. Add the following items to the config file**

- Add the following items to the bottom of your `config.txt` file

```
dtoverlay=vc4-kms-dpi-hyperpixel4

dtparam=rotate=90,touchscreen-swapped-x-y,touchscreen-inverted-y
```
**5. Save the changes**

- Save the changes to the `config.txt` file. 

**6. Now we will create a new file with the following command**

```
sudo nano /usr/share/X11/xorg.conf.d/monitor.conf
```
**7. Add the following to this new file**
```
Section "Monitor"
    Identifier "DPI-1"
    Option "Rotate" "right"
EndSection
```
> This new file `monitor.conf` will force Klipper screen to use the correct screen orientation. Without this, the Pi will start with the correct orientation however Klipper screen will default back to the default hyperpixel orientation and not the one defined in `/boot/config.txt`.

Thank you to @jacyhung for this solution who originally provided it on an issue thread here - https://github.com/pimoroni/hyperpixel4/issues/177

**8. Save `monitor.conf`**

- Save this new file. 

**9. Restart your Raspberry Pi**

- We recommend a full printer power cycle to restart your Raspberry Pi

**10. Witness the glory of your new screen! Ain't it beautiful ❤️**

- That's it, you should now have a working screen that looks fantastic! 

![Hyperpixel Mount - Image for GitHub 1  - 1](https://user-images.githubusercontent.com/58088168/210138461-019df19e-ae77-4082-b618-02178eacfe4c.jpeg)

## Share your build photos with us! 📸

Please share your build photos with us here. https://forms.gle/cWr6mDuEVakhQoQE9 

We won't post anything unless you grant us permission to do so! 

## Contributing

We would love anyone to contribute to this project, from design variants to cable clips, make it yours! 

## Acknowledgements

Thank you to the [Voron Design Team](https://vorondesign.com/) for designing such awesome printers! You guys rock 🤘🏻

Thanks to [Pimoroni](https://shop.pimoroni.com/) for making this awesome screen! Go check them out for more Raspberry Pi and maker goodness 🔩

Thanks to the [Klipper Screen Team](https://klipperscreen.readthedocs.io/en/latest/) for their great solution for interacting with Klipper! 🖥️ 

## Licence

Distributed under GNU General Public License version 3.0 (GPLv3)

## How to get in contact with us

Should you have any questions, changes, or issues about this repo or you just want to say hi, drop us an email here - **info@printup.xyz**

Our Director is also on Discord - Phalnix#3899

We'll have our own Discord Server later in Mid-Late 2023
