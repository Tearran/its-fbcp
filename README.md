# its-fbcp
## Include This Script "fbcp-ili9341" 
### About its-fbcp
 A method of setup for [juj](https://github.com/juj)'s [fbcp-ili9341](https://github.com/juj/fbcp-ili9341) Fast Display Frambuffer 

Advantages/Disatvantages:
- RE-compile without rm build directory contents
  - `cmake --clean-first`
  - `rm` may be more reliable
- system controle of fbcp
  - loads befor rc.local
- manual controle
  - SSH Start/Stop display driver
  - SSH Enable/Disable Auto Loading
  - Mixing projects
    - Stop fbcp to Start luma.lcd
    - GPIO Control of driver
    
## Reference 
Initial proof of concept video: [youtube](https://www.youtube.com/watch?v=h1jhuR-oZm0)

## Alternate Build example
With System Control of Frambuffer

## Build it
Here is a full example of what to type to build and run, if you have the Waveshare [1.3inch LCD HAT](https://www.waveshare.com/wiki/1.3inch_LCD_HAT) with ST7789VW controller:

```bash
{
cd ~
sudo apt-get install git cmake
git clone https://github.com/juj/fbcp-ili9341.git
cd fbcp-ili9341
mkdir build
cd build
cmake --clean-first -Wno-dev -DWAVESHARE_ST7789VW_HAT=ON -DSPI_BUS_CLOCK_DIVISOR=20 -DBACKLIGHT_CONTROL=OFF -DUSE_DMA_TRANSFERS=ON -DSTATISTICS=0 ..
make -j
}
```
## Test Binary

```bash 
sudo ./fbcp-ili9341
```
CTRL-C to exit
## Launching the display driver at startup
Install fbcp to /usr/bin/ 
```bash
sudo install $HOME/fbcp-ili9341/fbcp-ili9341 /usr/bin/fbcp
```
To set up the driver to launch at startup, creat a system service

NOTE: Changing "rc.local" to "loclal-files" Assumes mildly faster exucution of fbcp during bootup
  - TODO: test
Video Refrance:
  - TODO: [Youtube]()
```bash
{
#Startup configuration
sudo cat << EOF > /tmp/fbcpd.service

[Unit]
Description=Starts Frambuffer copy
DefaultDependencies=false

[Service]
Type=simple
ExecStart=fbcp
WorkingDirectory=/usr/bin/

[Install]
WantedBy=local-fs.target
EOF

sudo cp -f /tmp/fbcpd.service /etc/systemd/system/fbcpd.service 
sudo systemctl enable fbcpd.service
}
````
## Usefull Service command

- Enable/Disable service
  - `sudo systemctl enable fbcpd.service`
  - `sudo systemctl enable fbcpd.service`

- Start/Stop service
  - `sudo systemctl start fbcpd.service`
  - `sudo systemctl stop fbcpd.service`
  - `sudo systemctl restart fbcpd.service`
