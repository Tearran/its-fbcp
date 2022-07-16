## Build it
Here is a full example of what to type to build and run, if you have the Waveshare [1.3inch LCD HAT](https://www.waveshare.com/wiki/1.3inch_LCD_HAT)

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
## Test it

```bash 
sudo ./fbcp-ili9341
```
CTRL-C to exit

## Install it
Install fbcp to /usr/bin/ 
```bash
sudo install $HOME/fbcp-ili9341/build/fbcp-ili9341 /usr/bin/fbcp
```
## Start it
To set up the driver to launch at startup, creat a system service

```bash
{
# start of Make a temp C file for systemd && systemctrl
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
# end of Make a temp startup configuration file for systemd && systemctrl
#
# Copy temp startup configuration to System folder
  sudo cp -f /tmp/fbcpd.service /etc/systemd/system/fbcpd.service 
# Enable the daemon
  sudo systemctl enable fbcpd.service
# Start the daemon
  sudo systemctl start fbcpd.service

}
````
## Controle it
Usefull Service commands

- Enable/Disable service
  - `sudo systemctl enable fbcpd.service`
  - `sudo systemctl diable fbcpd.service`

- Start/Stop service
  - `sudo systemctl start fbcpd.service`
  - `sudo systemctl stop fbcpd.service`
  - `sudo systemctl restart fbcpd.service`

## Use it
include with:
  - bash scripts
  - python3
