# OGFX - Open Guitar Effects

A high level overview of the OGFX project.

## Rationale

The OGFX project aims to combine readily available software and easy to build hardware into a hackable, nerd-friendly, usable (guitar) effects platform.

## Software components

This is a broad overview of the software components of the system:

* nixos/nixpkgs are used as the base of the system
* a realtime kernel (PREEMT_RT_FULL).
* one instance of jalv (made by drobilla, the author of the LV2 plugin standard) per plugin
* LV2 plugins including guitarix, fomp, swh, zam, mda, ...
* jack2 a.k.a jackdmp
* hostapd and dnsmasq to turn the machine into an access point enabling editing setups from mobile devices
* ogfx-ui, the web frontend, written in python 3.7
* ogfx-tool, some helper tools, mostly c++

## OGFX is not ready yet

The system is useful for us but it is not useful for the general public yet. We will release a version 0.1 when we think this has changed.

## An overview of the other repositories:

- http://github.com/OGFX/nixpkgs A fork of nixpkgs from the NIXOS operating system. This repository contains a branch called ogfx-nixos-20.03 which is the one the OGFX system is based upon
- http://github.com/OGFX/ogfx-ui A web frontend for the OGFX system,
- http://github.com/OGFX/ogfx-tools Some tools supporting the ogfx-ui
- http://github.com/OGFX/jack2 A fork of jack2
- http://github.com/OGFX/ogfx-nixos-rpi4 This repository contains the nix expressions to generate a bootable SD card image containing the OGFX system
- http://github.com/OGFX/ogfx86 A x86 based variant nixos configuration
- https://github.com/OGFX/ogfx-midi-controller The firmware for a teensy based midi controller

## Found a bug? Report it!

If you know what component has the bug, then please file an issue in the respective repository's issue tracker. Otherwise just file the bug in this repository:

https://github.com/OGFX/ogfx-overview/issues

## I prepared the SD-card with the image and booted it - What now?

### Establish a network connection to the system

- You need to log into the system. There are mainly two ways:

  1. Plug in an ethernet cable. The system is configured to use DHCP from your network. It will, if local name resolution is supported by your router, be reachable under the hostname "ogfx". If not, look into your router's interface and find the device. You will need to use this way for the initial setup of the system because some software artifacts will have to be downloaded.
  
  2. Connect to the WIFI-network with ESSID "ogfx" which has been brought up by the system. Your device might complain about no internet access being available on this network - Connect to it anyways! The device will have the IP address 192.168.150.1. The passphrase is "omg it's fx"
  
After figuring out which of the two steps above you needed connect to the device via SSH on port 22 (the standard port). The username is "ogfx" and the password is "ogfx".

### Change passswords, ESSID

- Use an editor to change the file <code>/etc/nixos/configuration.nix</code>. At least <code>vim</code> and <code>nano</code> are included. The user "ogfx" is in the sudoers list, so use <code>sudo</code> to edit that file. The <code>networking</code> section has the hostname of the device. The <code>hostapd</code> section has the ESSID and passphrase for the WIFI access point. Change those to your liking.

- After changing configuration.nix run this command to instantiate the changes:

<pre>
sudo nixos-rebuild switch
</pre>

and reboot afterwards:

<pre>
sudo reboot
</pre>

After the system rebooted your changes should have been made. 

- Use the usual <code>passwd</code> command to change the password of the "ogfx" user.

### Change the USB device name

- Change the last argument in the <code>services.jack.jackd.extraOptions</code> line in <code>/etc/nixos/configuration.nix</code> to the ALSA pcm name of your USB device. Now run <code>nixos-rebuild switch</code> and reboot (or optionally run <code>sudo systemctl restart jack</code> and reattach your USB device. Use <code>journalctl -u jack</code> to check for jack's output and also <code>journalctl -u ogfx-frontend</code> to see if the ogfx web UI started.

### Point your browser to the system on port 8080

- Now you're ready to play with the system.

## Back up your <code>~/.local/share/ogfx</code> folder

- It has your setups and racks and things..

## What it looks like

### Hardware

This is fps' personal setup. Yours might look completely different.

![a photo](https://github.com/OGFX/ogfx-overview/raw/master/IMG_20200421_123438.jpg)

### Software

#### Desktop

![a screenshot](https://github.com/OGFX/ogfx-overview/raw/master/pic-20200718-070746.png)

#### Mobile

![another screenshot](https://github.com/OGFX/ogfx-overview/raw/master/Screenshot_20200718-073747_Firefox.png)

