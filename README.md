This project aims to explain how to set up a complete multimedia center (mediacenter), a game station and a download server. All in one. Any use aimed at hacking / stealing content with copyrights / third parties without express consent is prohibited. This project is based on a set of free software that can be easily found on the internet. This project has no lucrative purpose, its sole purpose is to teach and educate people the configuration and use of the different programs. This project was originally maintained by AikonCWD and has since stopped updating the project, so i am taking it on board to get it back up and running smoothly again. Obviously there will and are hick-ups/bugs. Thus for the mean time i will keep the project in Beta until we have a fully functional release. 
For DCMA reasons Kodi will be supplied with NO EXTRA ADD-ONS. Please do not ask about them Look HERE if you are such inclined to do so. We do not condone such behavior.

Features:
-Multi-Media Center: Kodi 17.4 Krypton
-Game Center: RetroPie 4.0
-Game Streaming: Moonlight 2.2.1
-Download Center(s): Transmission & PyLoad
-Workstation: XFCE, FireFox & Chromium
-Tools: a bunch of extra tools

Needed Components:
-RPi 2 or PRi3
-MicroSD SDHC card (6gb or more recommended)
-MicroUSB Charger(5Volt and 3Amp)
-Protective enclosure for the RPi
-HDMI Cable

Recommended Extras:
-Power supply cable with the ON/OFF click button switch
-Heat sinks and fan to help keep the RPi Cooler
-Wireless Keyboard and Mouse Combo
-Xbox360 Controller (USB)

Pre-Configured for ease of use:
-Everything is pre-configured for a plug and play functionality. You shouldn't have to set anything up unless you have updated the files.
-Everything is in English, Originally translated from Spanish. (Please note i can support more languages if its needed in the future)
-Protocols SSH and SMB (Samba) are enabled (Username: root / Password: aikoncwd)
-Transmission setup for maximum torrent speeds (IT IS HIGHLY RECCOMENDED TO SET THIS UP WITH YOUR OWN Username and Password! Info on how to do that can be FOUND HERE)
-Access via Zeroconf enabled (For remote control via SmartPhone)

Whats Been Disabled for Performance Reasons:
-AirPlay
-Time Addon
-RSS news reader disabled
-Library Sharing Via UPnP

Okay Lets get started with the Installation, its pretty straight forward i have shrunk the .img as low as i can for the mean time. After Beta is done i will make more of an effort to shrink the file further.

Installation:
1. Download the preconfigured BETA-RPiMediaCenter.img image
2. Record the image on your microSD card :
-Windows : Use Win32DisKImager
-Linux :
Code:
sudo pv BETA-RPiMediaCenter.img | sudo dd of=disk2s1 bs=4M && sync
-MAC : Use the Apple-PiBakery program , thanks to jagarciavi
3. Insert your microSD with the .IMG that we loaded on to the SD-Card In the previous step
4. Plug in the power
5. The Raspberry will light up (Red/Green LED's on the mainboard) and the start up splash will show.
7. RPi Media Center will start automatically at boot every time.
8. (Optional) Verify that the partition occupies 100% of your microSD with the command:
Code:
df -h
MD5 CHECK-SUM:
Code:
921d4d195a795ddef00cf221160836f6
*Verify on windows with this TOOL

After Install
It is recommended that you set-up a static IP for your Media Center. It makes things a whole lot easier if you're using Moonlight and Transmission.
Which can be done by:
Opening Terminal and Typing
Code:
nano /etc/dhcpcd.conf
Then removing # From each of these lines:
Code:
interface eth0
static ip_address=192.168.1.100/24
static routers=192.168.1.1
static domain_name_servers=8.8.8.8
And then setting up as to how you need it to. Its different for everyone.

Extras Install Guide:

Configure PyLoad (optional)
PyLoad is a program that allows you to transform your Raspberry into a direct download server . The PyLoad daemon is installed and configured, but it is disabled by default since not all users need to use it. If you want to enable and use PyLoad ... keep reading:

First of all we are going to configure the daemon so that it is auto-executed when turning on the Raspberry . Edit the cron auto-boot file with the command:

Code:
crontab -e
We are located at the bottom, locate the line @reboot pyLoadCore -daemonand remove the comment from the beginning, it should look like this: @reboot pyLoadCore --daemon( you have to put the 2 dashes in front of the word daemon ). Save the changes by pressing the keys: CTRL+ X, then Yand finallyIntro

You will have to restart your Raspberry to have the pyLoad daemon running, remember that Kodi turns on automatically, you must close it to return to the console.

We access PyLoad through a web browser using port 8000 , for example: http://192.168.1.100:8000
The default user is root and password root . In the top menu you can manage the user and change the password (recommended), just below you will find the configuration where you can edit the configuration, captchas plugins etc ... and add any premium account you have from the different hosts.

Overclocking (optional) DO SO AT YOUR OWN RISK!
I recommend enabling a bit of overclock , you'll get more fluency when moving through the Kodi menus and you'll noticeably boost performance when playing emulators. Your CPU will be able to perform faster calculations and access to ram memory or microSD disk will have lower response times. 
Strongly recommend use some method of ventilation / cooling in order to avoid reaching 85C , since the RPI lower speed if it reaches that temperature

If you want you can run a benchmark (diagnostic) to test your overclock level, execute the following command:

Code:
curl https://raw.githubusercontent.com/ai...i-benchmark.sh | sudo bash
Raspberry Pi 3: Overclock settings
Edit your file nano /boot/config.txtand paste the following code, you can adjust the values ​​to have more or less overclock:

Code:
force_turbo=0                   #Enable cpu-overclock over 1300MHz (default 0)
avoid_pwm_pll=1                 #Enable no-relative freq between cpu and gpu cores (default 0)

arm_freq=1300                   #Frequency of ARM processor core in MHz (default 1200)
core_freq=550                   #Frequency of GPU processor core in MHz (default 400)
over_voltage=6                  #ARM/GPU voltage adjust, values over 6 voids warranty (default 0)

sdram_freq=575                  #Frequency of SDRAM in MHz (default 450)
sdram_schmoo=0x02000020         #Set SDRAM schmoo to get more than 500MHz freq (default unset)
over_voltage_sdram_p=6          #SDRAM phy voltage adjust (default 0)
over_voltage_sdram_i=4          #SDRAM I/O voltage adjust (default 0)
over_voltage_sdram_c=4          #SDRAM controller voltage adjust (default 0)

gpu_mem=256                     #GPU memory in MB. Memory split between ARM and GPU (default 64?)
gpu_freq=550                    #Sets core_freq h264_freq isp_freq v3d_freq together (default 300)
v3d_freq=500                    #Frequency of 3D block in MHz (default ?)
h264_freq=350                   #Frequency of hardware video block in MHz (default ?)

dtparam=sd_overclock=75         #Clock in MHz to use for MMC micrSD (default 50)
dtparam=audio=on                #Enables the onboard ALSA audio (always use this ON)
dtparam=spi=on                  #Enables the SPI interfaces (default OFF)

temp_limit=80                   #Overheat protection. Disable overclock if SoC reaches this temp
initial_turbo=60                #Enables turbo mode from boot for the given value in seconds

hdmi_drive=2                    #Normal HDMI mode. Sound will be sent if supported and enabled (default 2)
hdmi_ignore_cec_init=1          #Avoids bringing TV out of standby and channel switch when booting (default 0)
hdmi_ignore_cec=0               #Pretends CEC is not supported. No CEC functions will be supported (default 0)
hdmi_force_hotplug=1            #Pretends HDMI hotplug signal is asserted (default 0)

start_x=1                       #Enable software decoding (MPEG-2, VC-1, VP6, VP8, Theora, etc. default 0)
overscan_scale=1                #Video Output will respect the overscan settings (default 1)
disable_overscan=0              #Disable overscan configuration. Set 1 if you see black lines on TV (default 0)
disable_splash=1                #Avoids the rainbow splash screen on boot (default 0)
avoid_warnings=1                #Disable warnings (Red=over-temperature ; Rainbow=under-voltage). (default 0)

gpu_mem_256=128
gpu_mem_512=256
gpu_mem_1024=256
Read the commands well, you may want to modify some to customize your image.

Raspberry Pi 2: Overclock settings
Edit your file nano /boot/config.txtand paste the following code, you can adjust the values ​​to have more or less overclock:

gpu_mem=256
gpu_mem_256=128
gpu_mem_512=256
gpu_mem_1024=256

arm_freq=1100
core_freq=550
sdram_freq=483
over_voltage=6
over_voltage_sdram=2
temp_limit=70
force_turbo=0
initial_turbo=60

hdmi_drive=2
hdmi_ignore_cec=0
hdmi_ignore_cec_init=1
hdmi_ignore_hotplug=0
hdmi_force_hotplug=1

#disable_overscan=0
#overscan_scale=1

#overscan_left=49
#overscan_right=49
#overscan_top=29
#overscan_bottom=25

max_usb_current=1
dtparam=audio=on
dtparam=spi=on
You will find a script called bcmstat that allows you to accurately measure the hardware status of your Raspberry, you can see at what speed your CPU is going and at what temperature it is, for this it executes:

/root/bcmstat.sh

MoonLight
*Coming Soon*

DOWNLOAD

Download Option#1 https://drive.google.com/open?id=1ZTBroQ5Pp8JUyUOdYEoLRYQOK3vSW2Hs
Download Option#2 http://www.mediafire.com/file/dc31c8od4272r63/RPiMediaCenter.img

Credits:
AikonCWD for his amazing original work
@Valkiry for continuing the development


BUGS
-Desktop/Emulationstation and wifi addons are currently not working.
Just use These commands for what you need when it goes to the terminal:

Desktop Environment:
Code:
startx
RetroPie:
Code:
emulationstation
Wifi 
Code:
./RetroPie-Setup/retropie_packages.sh 829 gui
Bluetooth
Code:
 ./RetroPie-Setup/retropie_packages.sh 803 gui
I will fix these at a later date :) But for the mean time let me know how you go :)


Also apologies for teh crappy layout ill fix it up later
Here is my XDA Post https://forum.xda-developers.com/raspberry-pi/development/mediacenter-rpi-media-center-beta-t3768793/post76018850#post76018850
