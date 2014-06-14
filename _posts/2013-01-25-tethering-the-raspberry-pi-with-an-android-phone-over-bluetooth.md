---
layout: post
title: "Tethering the Raspberry Pi with an Android Phone over Bluetooth"
description: ""
category: "PiHUD"
tags: [Raspberry Pi]
---
{% include JB/setup %}

AI am tethering my Raspberry Pi with my Android phone over Bluetooth for internet connectivity.

I used the Kinivo BTD-300 Bluetooth 3.0 USB dongle, which works right out of the box.

Here are the steps I used to get tethering working:

1. Install bluetooth packages:
2. apt-get install bluetooth bluez-utils blueman?bluez-compat
3. Check if the USB dongle is detected with lsusb
4. Run the /etc/init.d/bluetooth status command to check if bluetooth is running. The output should be something like this: Bluetooth is running.
5. Turn your phone’s bluetooth on and set it to be visible. Scan for it with: hcitool scan. Your phone’s name and MAC address should appear.
6. Pair the two devices by running bluetooth-agent 1234, replacing ’1234′ with a PIN code of your choice. Connect to the Pi from the phone.
7. List all the devices that are paired using sudo bluez-test-device list. The phone should appear in the list if it was successful.
8. Create a PAN connection with: sudo pand -c --role PANU --persist 30.
9. Add the following line to /etc/network/interfaces: iface bnep0 inet dhcp

Your Pi should now be tethered! Add the pand line to /etc/rc.local to have it automatically begin on startup. The persist option means it will try to reconnect every 30 seconds if the signal is lost.
