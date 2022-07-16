# its-fbcp
## Include This Script "fbcp-ili9341" 
### About it
its-fbcp
Setup for [juj](https://github.com/juj)'s [fbcp-ili9341](https://github.com/juj/fbcp-ili9341) Fast Display Frambuffer 

Here is Full examples of what to type to build and run, if you have the

- Waveshare: 
  - [ 1.3inch LCD HAT ] - [Full example](https://github.com/Tearran/its-fbcp/edit/main/fbcp-gamepi13/README.md)
  - TODO: [ GamePi20 ]
  - TODO: [ ST7789vw ]
  - TODO: [ st7789s ] ??
  
This method offfers:
- system controle of fbcp
  - loads befor rc.local
- manual controle
  - SSH Start/Stop display driver
  - SSH Enable/Disable Auto Loading
  - Switching display drivers
    - ie: Stop fbcp to Start luma.lcd
