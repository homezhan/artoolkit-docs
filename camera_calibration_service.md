#Camera Calibration Service
Every device uses a different camera, and each of these cameras have variables which effect the ability of ARToolKit (and all computer vision) to work properly. The camera calibration service is a cloud-and-crowd-based solution to generating and retreiving these camera-specific variables. 

##What Information is Collected?
This service does not store or transmit any personally identifying
information.

If a network connection is available, the following information may be
transmitted to an ARToolworks server for the purpose of retrieving
camera calibration information for your specific Android device:

-   The make and model of device (e.g. Samsung Galaxy S).
-   Which camera on the device is being used.

No personally identifying data is transmitted or stored during as part
of the process. Additionally, the data is transferred via a secure HTTPS
connection.

##How do I Contribute to the Service?
Currently, the service is used exclusively on the Android platform through the [Camera Calibration App for Android][calib_app]. 

[Category:Tools](/Category:Tools "wikilink")
[calib_app]:/camera_calibration_for_android