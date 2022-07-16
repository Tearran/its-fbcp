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
  - switching display drivers
    - Stop fbcp to Start luma.lcd
    
