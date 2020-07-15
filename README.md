# ogfx-overview

A high level overview of the OGFX project.

# Rationale

Since the new Raspberry Pi4 dropped we were amazed to find that it finally offers a working USB3 host which can drive an USB class audio 2.0 device. 

The system image is based on nixos/nixpkgs. The code to reproduce them can be found in the other repos in the OGFX organization.

The OGFX project aims to combine readily available software and easy to build hardware into a hackable, nerd-friendly, usable guitar effects platform.

# OGFX is not ready yet

The system is useful for us but it is not useful for the general public yet. We will release a version 0.1 when we think this has changed.

# What it looks like

![a photo](https://github.com/OGFX/ogfx-overview/raw/master/IMG_20200421_123438.jpg)

# An overview of the other repositories:

- http://github.com/OGFX/nixpkgs A fork of nixpkgs from the NIXOS operating system. This repository contains a branch called ogfx-nixos-20.03 which is the one the OGFX system is based upon
- http://github.com/OGFX/ogfx-ui A web frontend for the OGFX system,
- http://github.com/OGFX/ogfx-tools Some tools supporting the ogfx-ui
- http://github.com/OGFX/jack2 A fork of jack2
- http://github.com/OGFX/ogfx-nixos-rpi4 This repository contains the nix expressions to generate a bootable SD card image containing the OGFX system

# I prepared the SD-card with the image and booted it - What now?

## Establish a network connection to the system

- You need to log into the system. There are mainly two ways:

  1. Plug in an ethernet cable. The system is configured to use DHCP from your network. It will, if local name resolution is supported by your router, be reachable under the hostname "ogfx". If not, look into your router's interface and find the device. You will need to use this way for the initial setup of the system because some software artifacts will have to be downloaded.
  
  2. Connect to the WIFI-network with ESSID "ogfx" which has been brought up by the system. Your device might complain about no internet access being available on this network - Connect to it anyways! The device will have the IP address 192.168.150.1. The passphrase is "omg it's fx"
  
After figuring out which of the two steps above you needed connect to the device via SSH on port 22 (the standard port). The username is "ogfx" and the password is "ogfx".

## Change passswords, ESSID

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

## Change the USB device name

- Change the last argument in the <code>services.jack.jackd.extraOptions</code> line in <code>/etc/nixos/configuration.nix</code> to the ALSA pcm name of your USB device. Now run <code>nixos-rebuild switch</code> and reboot (or optionally run <code>sudo systemctl restart jack</code> and reattach your USB device. Use <code>journalctl -u jack</code> to check for jack's output and also <code>journalctl -u ogfx-frontend</code> to see if the ogfx web UI started.

# Point your browser to the system on port 8080

- Now you're ready to play with the system.

# Back up your <code>/etc/nixos/configuration.nix</code>

- Even if you have to reflash a new SD card with the original OGFX image: Afterwards just copy your <code>configuration.nix</code> back over and your system should be ready to go. 

# Back up your <code>~/.local/share/ogfx</code> folder

- It has your setups and racks and things..
