
The driver for the oem7:  
https://github.com/novatel/novatel_oem7_driver   
  
I believe the model we have has the oem6 reciever. The oem7 driver did not work but if it is supposed to then it might have to do with how it is configured.  
http://wiki.ros.org/novatel_oem7_driver  
the ros wiki has some information about how to get it started.  
  
I think this is the model:  
https://www.navtechgps.com/novatel_flexpak6_enclosure/  
  
  
  
  
____________________________________________________________________________________________________________________________________________  
https://github.com/swri-robotics/novatel_gps_driver/tree/master  
This driver says it should work with the oem6 however I am getting this error: [ERROR] [1725578278.765605678]: insufficient data rate <Novatel GPS (/dev/ttyUSB0)>: 5.000000 < 20.000000  
https://github.com/swri-robotics/novatel_gps_driver/issues/44  
This thread says to change expected_rate_(20) in novatel_gps_nodelet.cpp to lower (they said 0.5 worked). However I cannot find this file when downloading using apt  
It does exist ont the github page so I built it from source in the novatel workspace on the pi.  
I changed the value and it publishes messages on the /fix topic however it says it is at longitude and latidue (0,0)  
some errors it gives are:  
- Unexpected binary message id  
- insufficient data rate <Novatel GPS (/dev/ttyUSB1)>: 0.000000 < 0.500000  
I would recommend playing with the values a bit. Possibly change the input to ttyUSB2 or ttyUSB3

**#44 also linked to https://github.com/swri-robotics/novatel_gps_driver/issues/6#issuecomment-403187704                                      
This one suggest to get the novatel connect software and configure the hardware. This seems to be the actual fix for https://github.com/swri-robotics/novatel_gps_driver/                             
page to download novatel software: https://novatel.com/support/support-materials/software-downloads**                                                                              
                                                                                                                                              
**"I have been able to get past this issue. The issue is caused by the configuration of your specific hardware.                                  
In order to fix this issue you will need to have access to the Novatel Connect software (requires a Windows OS).                              
The fix requires that you configure the correct Serial/USB ports to output Novatel data (this can be configured under the COM PORT Wizard).   
The SWRI Novatel ROS package has a launch file tester_for_usb.launch which has usb0 set as default.                                           
Keep in mind that Novatel hardware has USB1, USB2... and COM1, COM2,... but linux systems recognize USB and COM ports on a zero-base system."**
____________________________________________________________________________________________________________________________________________  
  
  
  
  
  
  
lastly if that somehow does not work then try https://github.com/ros-drivers/novatel_span_driver  
I could not get this to work as I encountered a lot of outdated packages that needed to be installed  
