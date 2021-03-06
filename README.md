# LGTVCompanion

DESCRIPTION
    <<<< LGTV Companion >>>>

    The application (UI and service) controls your WebOS (LG) Television.

    Using this application allows for your WebOS display to shut off and turn on
    in reponse to to the PC shutting down, rebooting, entering low power modes as well as 
    and when user is afk (idle). Like a normal PC-monitor. Or, alternatively this application 
    can be used as a command line tool to turn your displays on or off.

BACKGROUND
    With the rise in popularity of using OLED TVs as PC monitors, it is apparent that standard
    functionality of PC-monitors is missing. Particularly turning the display on or off in 
    response to power events in windows. With OLED monitors this is particularly important to 
    prevent "burn-in", or more accurately pixel-wear.

INSTALLATION AND USAGE
    0) Important prerequisites:
        a) Power ON all TVs
        b) Ensure that the TV can be woken via the network. For the CX line of displays this is 
          accomplished by navigating to Settings (cog button on remote)->All Settings->Connection->
          Mobile Connection Management->TV On with Mobile and enable ''Turn On via Wi-Fi'.
        c) Open the admin interface of your router, and set a static DHCP lease for your WebOS 
          devices, i.e. to ensure that the displays always have the same IP-address on your LAN.

    1) Download the setup package and install. This will install and start the service 
    (LGTVsvc.exe), and also install the user interface (LGTV Companion.exe).

    2) Open the user interface from the Windows start menu.

    3) Click the 'Scan' button to let the application try and automatically find network attached WebOs 
    devices (TVs)

    4) Optionally, click the drop down button to manually add, remove, configure the parameters of respective 
    devices, this includes the network IP-address, and the physical address, i.e. the MAC(s). This information
    can easily be found in the network settings of the TV.

    5) In the main application window, use the checkboxes to select what power events (shutdown, restart, 
    suspend, resume, idle) the respective devices shall respond to.

    6) Optionally, tweak additional settings, by clicking on the hamburger icon. Note that enabling logging can 
    be very useful if you are facing any issues.
    
    IMPORTANT NOTICE: if your OS is not localised in english, you must in the 'additional settings'
    dialog click the correct checkboxes to indicate what words refer to the system restarting/rebooting
    (as opposed to shutting down). This is needed because there is no better (at least known to me) 
    way for a service to know if the system is being restarted or shut down than looking at a certain event 
    in the event log. But the event log is localised, and this approach saves me from having to build a language 
    table for all languages in the world. Note that if you don't do this on a non-english OS the application
    will not be able to determine if the system is being restarted or shut down. The difference is of course 
    that the displays should not power off when the system is restarted.

    7) Click Apply, to save the configuration file and automatically restart the service. 
    
    8) At this point your respective WebOS TV will display a pairing dialog which you need to accept.
    
    All systems are now GO!

    9) Please go ahead and use the drop down menu again and select 'Test', to ensure that the displays 
    properly react to power on/off commands.


LIMITATIONS
    The OLED displays cannot be turned on via network when an automatic pixel refresh is being performed. You can hear 
    an internal relay click after the display is actually powered down, at which point it can be turned on again at any 
    time by the application.

    The WebOS displays can only be turned on/off when both the PC and the display is connected to a network. 


SYSTEM REQUIREMENTS
    - The application must be run in a modern windows environment, i.e. any potato running Windows 10 is fine.
    - A LAN

COMMAND LINE ARGUMENTS

    LGTV Companion.exe -[poweron|poweroff|autoenable|autodisable] [Device1|Name] [Device2|Name] ... [DeviceX|Name]

    -poweron        - power on a device.
    -poweroff       - power off a device
    -autoenable     - temporarily enable the automatic management of a device, i.e. to respond to power events. This
                      is effective until next restart of the service. (I personally use this for my home automation system).
    -autoenable     - temporarily disable the automatic management of a device, i.e. to respond to power events. This
                      is effective until next restart of the service. 

    [DeviceX|Name]  - device identifier. Either use Device1, Device2, ..., DeviceX or the friendly device name as found 
                      in the User Interface, for example OLED48CX.

    Example usage: LGTV Companion.exe -poweron Device1 Device2 OLED48CX -autodisable Device4 

    This command will power on device 1, device 2 and the device named OLED48CX, and additionally device4 is set to 
    temporarily not respond to automatic power events (on/off).

ADDITIONAL NOTES
    N/A

CHANGELOG
    v 1.0.0            Initial release

LICENSE
    Copyright (c) 2021 Jörgen Persson
    
    Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation 
    files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, 
    modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the 
    Software is furnished to do so, subject to the following conditions:

    The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE 
    WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR 
    COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, 
    ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

THANKS TO
    - Niels Lohmann - JSON for Modern CPP https://github.com/nlohmann/json
    - Boost libs - Boost and Beast https://www.boost.org/
    - Maassoft for initial inspo and helping me understand the WebSocket/WebOS comms - https://github.com/Maassoft

COPYRIGHT
    Copyright (c) 2021 Jörgen Persson
