# The Things Network: RAK833-based gateway

Reference setup for [The Things Network](http://thethingsnetwork.org/) gateways based on the RAK833 USB/SPI concentrator with a Raspberry Pi host using the RAK833 SPI adapter PCB.

## Setup based on standard MyPi Integrator Board Raspbian image

- Plug in the RAK833 Adapter PCB with the RAK833 module connected
- Start your RPi connected to Ethernet
- From a computer in the same LAN, `ssh` into the RPi using default `pi` user (for IP address see HMDI output)

        local $ ssh pi@192.168.1.135

- Default password  for user `pi` is `raspberry`
- Edit /boot/config.txt and add the line below to the bottom to enable the SPI interface (or alternately use `raspi-config`) 

        dtparam=spi=on
        
- Reboot
- Make sure you have an updated installation and install `git`:

        $ sudo apt-get update
        $ sudo apt-get upgrade
        $ sudo apt-get install git

- Create new user for TTN and add it to sudoers

        $ sudo adduser ttn
        $ sudo adduser ttn sudo

- Logout and login as `ttn` and remove the default `pi` user

        $ sudo userdel -rf pi

- Ethernet connection is recommended, if you still want to use WiFi configure the WiFi credentials (check [here for additional details](https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md))

        $ sudo nano /etc/wpa_supplicant/wpa_supplicant.conf

        network={
            ssid="The_SSID_of_your_wifi"
            psk="Your_wifi_password"
        }

- Clone the installer and start the installation

        $ git clone git clone https://github.com/mypiandrew/rak833-spi.git
        $ cd rak833-spi/install
        $ sudo chmod +x *.sh
        $ sudo ./install.sh

- If you want to use the remote configuration option, please make sure you have created a JSON file named as your gateway EUI (e.g. `B827EBFFFE7B80CD.json`) in the [Gateway Remote Config repository](https://github.com/ttn-zh/gateway-remote-config).



# Credits

Credits for [gonzalocasas](https://github.com/gonzalocasas) and [ttn-zh](https://github.com/ttn-zh) for their installation procedure for the IMST iC880a. Also, that procedure is largely based on the awesome work by [Ruud Vlaming](https://github.com/devlaam) on the [Lorank8 installer](https://github.com/Ideetron/Lorank).
