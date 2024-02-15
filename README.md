# Raspberry-Pi-5-ST7789-usage
A short documentation on how to get ST7789[V3] SPI display working on the Raspberry Pi 5

Test environment:
* Raspberry Pi 5 Model B 4GB with Debian 12 (bookworm) kernel 6.1.0-rpi7-rpi-2712
* 280x240 ST7789V3 1.69" display module connected to the GPIO (rounded edges, bought from [aliexpress](https://www.aliexpress.com/item/1005005921876295.html))
  * Reset is not connected
  * CS -> CE0 (GPIO 7)
  * SCL -> SCLK (GPIO 11)
  * SDA -> MOSI (GPIO 10)
  * BLK -> GPIO 22 (can be configured in the config.txt)
  * DC -> GPIO 25 (can be configured)
  * VCC -> 3.3V
  * GND -> GND

### 1. Get the Adafruit installer scripts
```bash
git clone https://github.com/adafruit/Raspberry-Pi-Installer-Scripts
cd Raspberry-Pi-Installer-Scripts
```

### 2. Run the commands in "Prepare your system" section
```bash
sudo apt-get install python3-pip
sudo pip3 install --upgrade click
sudo pip3 install --upgrade setuptools
sudo pip3 install --upgrade adafruit-python-shell
```

### 3. Use the adafruit-pitft.py script
```bash
sudo python3 adafruit-pitft.py
```

### 4. Install with options
* Select option 6 (without touchscreen)
* Select no console (this might not appear)
  * In case there's only text mode available, make sure that you are running the version of Raspbian OS that has desktop environment
* Select reboot now

### 5. Configure the right options
```bash
sudo nano /boot/firmware/config.txt
```
* Make sure that hdmi_cvt has the right resolution
* Make sure that the same resolution is set in dtparam at the end of the config.txt

And after saving the config and rebooting the display should work right.

**p.s. at least on my display there is an offset issue (right side is missing 40px), if someone figures this out lmk!**
