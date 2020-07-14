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
