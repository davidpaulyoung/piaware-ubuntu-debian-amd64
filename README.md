## Automated Installation of <ins>_latest version_</ins> of piaware, dump1090-fa, piaware-web, and dump978-fa (by building packages from source code), on following OS: </br>

### (1) Ubuntu 18, 20, 22, & 23 - amd64 / x86_64  
### (2) Debian 9, 10, 11, & 12 - amd64 / x86_64  
### (3) Linux Mint 19, 20, & 21 - amd64 / x86_64  
### (4) Kali-linux 2021, 2022, & 2023 - amd64  
### (5) On RPI Model 3 & 4 (32-bit & 64-bit / armv7l & aarch64) Raspberry Pi OS Stretch, Buster, & Bullseye, DietPi OS Stretch, Buster, Bullseye, & Bookworm, Ubuntu 18, 20, and 22 for RPi, and Kali 2021 for RPi 
### (6) On RPI <ins>Model 5</ins> Raspberry Pi OS Bookworm (32-bit & 64-bit) </br>

## (1) DUMP1090-FA
**IMPORTANT NOTE:** </br>
Raspberry Pi OS **Bookworm** relesed on 2023-10-10 has broken USB on RPi4, but is OK on RPi5. </br>If you have installed Raspberry Pi OS **Bookworm** (2023-10-10) on RPi4, then to fix this bug, upgrade it by following commands: </br>
```
sudo apt update
sudo apt upgrade
sudo reboot
```
Copy-paste following command in SSH console and press Enter key. The script will install dump1090-fa. </br></br>
`sudo bash -c "$(wget -O - https://raw.githubusercontent.com/abcd567a/piaware-ubuntu-debian-amd64/master/install-dump1090-fa.sh)" `</br></br>


## (2) PIAWARE 
Copy-paste following command in SSH console and press Enter key. The script will install piaware. </br></br>
`sudo bash -c "$(wget -O - https://raw.githubusercontent.com/abcd567a/piaware-ubuntu-debian-amd64/master/install-piaware.sh)" `</br></br>

## (3) PIAWARE-WEB
Copy-paste following command in SSH console and press Enter key. The script will install piaware-web. </br></br>
`sudo bash -c "$(wget -O - https://raw.githubusercontent.com/abcd567a/piaware-ubuntu-debian-amd64/master/install-piaware-web.sh)" `</br></br>


## (4) DUMP978-FA (For USA ONLY. Requires 2nd Dongle)
If you want to receive both ES1090 and UAT978, then two dongles are required, one for 1090 MHz and other for 978 MHz. </br>
### (4.1) Copy-paste following command in SSH console and press Enter key. The script will install dump978-fa and skyaware978: </br>
`sudo bash -c "$(wget -O - https://raw.githubusercontent.com/abcd567a/piaware-ubuntu-debian-amd64/master/install-dump978-fa.sh)" `</br></br>

### (4.2) Serialize dongles as follows </br>
If you want to receive both ES1090 and UAT978, then two dongles are required, one for 1090 MHz and other for 978 MHz. In this case you will have to serialize dongles so that correct dongle+antenna sets are used by dump1090-fa and dump978-fa. </br></br>

For 1090 Mhz dongle: use serial # 00001090 </br>
For 978 Mhz dongle : use serial # 00000978 </br></br>


(4.1.1) Issue following command to install serialization software: </br>
`sudo apt install rtl-sdr` </br></br>
**(4.1.2) Unplug ALL DVB-T dongles from RPi** </br></br>
(4.1.3) Plugin only that DVB-T dongle which you want to use for dump1090-fa. All other dongles should be unplugged. </br></br>
(4.1.4) Issue following command. Say yes when asked for confirmation to chang serial number. </br>
`rtl_eeprom -s 00001090` </br></br>
**(4.1.5) Unplug 1090 dongle** </br></br>
(4.1.6) Plugin only that DVB-T dongle which you want to use for dump978-fa. All other dongles should be unplugged. </br></br>
(4.1.7) Issue following command. Say yes when asked for confirmation to chang serial number. </br>
`rtl_eeprom -s 00000978` </br></br>
**(4.1.8) Unplug 978 dongle** </br></br>
**IMPORTANT:** After completing above commands, unplug and then replug both dongles. </br>

### (4.3) - Configure dump1090-fa & dump978-fa to use dongles of assigned serial numbers </br>
```
sudo sed -i 's/^RECEIVER_SERIAL=.*/RECEIVER_SERIAL=00001090/' /etc/default/dump1090-fa  
sudo sed -i 's/driver=rtlsdr[^ ]* /driver=rtlsdr,serial=00000978 /' /etc/default/dump978-fa  
```

### (4.4) - Reboot so that dump1090-fa & dump978-fa can pick their assigned dongles at boot </br>

`sudo reboot `   </br>



