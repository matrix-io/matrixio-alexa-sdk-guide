# Alexa SDK Guide with MATRIX Creator/Voice

Guide on how to setup the Alexa SDK in a Raspberry Pi with a MATRIX Creator/Voice.

### Required Hardware

Before get started, let's review what you'll need.
* Raspberry Pi 3 (Recommended) or Pi 2 Model B (Supported).
* MATRIX Voice or MATRIX Creator - Raspberry Pi does not have a built-in microphone, the MATRIX Voice / Creator have an 8 mic array - Buy MATRIX Voice / MATRIX Creator. 
* Micro-USB power adapter for Raspberry Pi.
* Micro SD Card (Minimum 8 GB) - An operating system is required to get started. You can download Raspbian Stretch and use the guides for Mac OS, Linux and Windows in the Raspberry Pi website.
* External Speaker with 3.5 mm audio cable.
* A USB Keyboard & Mouse, and an external HDMI Monitor - we also recommend having a USB keyboard and mouse as well as an HDMI monitor handy. You can also use the Raspberry Pi remotely, see this guide from Google.
* Internet connection (Ethernet or WiFi)
(Optional) WiFi Wireless Adapter for Pi 2. Nyyote: Pi 3 has built-in WiFi.

First, this guide can take around an hour to install all packages and build the Alexa SDK. We have made an image with all packages installed and part of the SDK already built that takes that time to just few minutes. We recommned following the full guide in this readme, it will make you see how everything is installed and build but. If you are really in a hurry, the version of this guide using a pre-built image is [here](https://github.com/matrix-io/matrixio-alexa-sdk-guide/blob/master/matrix-alexa-guide-using-image.md).

### Let's get started

Once you have the Raspberry Pi with the SD Card inserted, the MATRIX board connected to it, power up the Raspberry Pi and open a terminal either in the Raspbian Desktop or just by ssh into it ( if you are you are using the Raspbian Lite version, in this case see guide on how to ssh [here](https://www.raspberrypi.org/documentation/remote-access/ssh/) ).

### 1. Installing MATRIX software

In order to allow the Google Assistant software to have access to MATRIX Voice microphones you need to first install:

```
# Add repo and key
curl https://apt.matrix.one/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.matrix.one/raspbian $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/matrixlabs.list

# Update packages and install
sudo apt-get update
sudo apt-get upgrade

# Installation MATRIX Pacakages
sudo apt install matrixio-creator-init
# Installation Kernel Packages
sudo apt-get -y install raspberrypi-kernel-headers raspberrypi-kernel git 
# Reboot
sudo reboot 
```
After reboot reconnect. Clone and build the kernel modules:

```
git clone https://github.com/matrix-io/matrixio-kernel-modules
cd matrixio-kernel-modules
make && make install
echo "dtoverlay=matrixio" | sudo tee -a /boot/config.txt
echo "matrixio-everloop" | sudo tee -a /etc/modules

# Reboot again
sudo reboot
```

Wait a bit and try to reconnect again.

### 2. Register a Product in Amazon Developer 

You'll need to register a device and create a security profile at  Amazon developer website. If you already have a registered product that you can use for testing, feel free to skip ahead. If not, follow step-by-step instructions [here](https://github.com/alexa/alexa-avs-sample-app/wiki/Create-Security-Profile).

#### IMPORTANT: 

For Allowed origins use: `http://localhost:3000` and `https://localhost:3000`. 
For Allowed Return URLs use `http://localhost:3000/authresponse` and `https://localhost:3000/authresponse`.

### 3. Install Alexa SDK

Download the install script. We recommend running these commands from the home directory (`~/`) or Desktop; however, you can run the script anywhere.

```
wget https://raw.githubusercontent.com/matrix-io/avs-device-sdk/master/tools/RaspberryPi/setup.sh
wget https://raw.githubusercontent.com/matrix-io/avs-device-sdk/master/tools/RaspberryPi/config.txt
```

Open the file in a editor and use the `Client ID`, `Product ID` and `Client Secret` from the registration steps to fill the file `config.txt`. Check [here](https://www.raspberrypi.org/magpi/edit-text/) If you need help editing the file.

Run the setup script with your configuration as an argument:
```
bash ./setup.sh ./config.txt
```
This installation can take some time,  about an hour, so go find something useful to do while waiting :)

After the setup script has finished running, you'll need to generate an authorization token. Run this command, and open your browser and navigate to `http://localhost:3000`. Log in with your Amazon credentials and follow the instructions provided:
```
bash ./startauth.sh
```

### 4. Run Alexa!

Let's run the Sample App:
```
bash ./startsample.sh
```

The output should be similar to [example-output.txt](https://github.com/matrix-io/matrixio-alexa-sdk-guide/blob/master/example-output.txt).
