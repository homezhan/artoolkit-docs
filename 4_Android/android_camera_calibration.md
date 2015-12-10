#Camera Calibration App for Android
For augmented reality to work properly on a device, we need to know some information about that device's camera. The ["ARToolKit Camera Calibrator" app][playstore] allows ARToolKit to better understand the camera and lens on your Android device. Producing good quality calibrations using this app can be used to improve ARToolKit tracking on your device.

All data captured in this app goes into the ARToolKit lens calibration data server, to help everyone who uses the same type of phone as you do augmented reality with ARToolKit.

##Requirements
* *The ["ARToolKit Camera Calibrator" app][playstore] requires Android v2.2 or later.*
* The PDF of the calibration file to print- either in [A4][patterna4] or [US Letter][patternus] size.
* A printer is required to print the calibration pattern.
* A network connection (e.g. wifi or cellular data) is required to upload the data. Without this, the app does not serve any useful purpose.


##How it Works
The calibration pattern consists of a grid of black and white squares surrounded by a white border. Due to how camera lenses work, when straight lines are viewed through the camera lens, they will naturally bend in accordance to the hemisphere of the lens itself. The ["ARToolKit Camera Calibrator" app][playstore] locates the corners of the squares and then measures the spacing between the corners and uses this information to calculate the lens distortion. The more images captured, and the more angles they are captured from, the lower the error in the distortion measurement. For this reason, in this app we capture 10 images.

###Get and Print the Pattern
1.   Download the calibration chessboard in [A4][patterna4] or [US Letter][patternus] size.
    -   (OPTIONAL) The calibration chessboards can also be found under the `doc/patterns` folder of the ARToolKit SDK as `Calibration chessboard (A4).pdf`, or `Calibration chessboard (US Letter).pdf`, respectively.
    -   (OPTIONAL) The calibration chessboards can also be printed from the app (via Google Cloud Print service) by selecting the "Print" button from app. To access the Print button, press the hardware menu button on the device or use the menu button on the Action Bar at the top of the screen (it looks like three vertical dots).
2.   Print the calibration chessboard you downloaded *at 100% sizing*, and be sure that no clipping of the pattern occurs.
![An example of the print dialog on Mac OS X, showing the PDF being printed at 100% of its size.][print_dialog]

When preparing your environment for calibrating your camera, there are a couple of best practices to keep in mind:

-   Since the chessboard pattern is assumed to be flat, *make sure that the chessboard pattern lays completely flat*.
    -   We recommend you firmly affix the chessboard to a flat surface (such as a table or piece of acrylic) using spray adhesive or double-sided tape. Very thick card stock also works well.
-   Make sure that the chessboard pattern is in a well-lit area, and is not obscured or occluded in any way.


###Get and Launch the App
[![The "ARToolKit Camera Calibrator" app in the Google Play Store.][play_store]][playstore]
[The "ARToolKit Camera Calibrator" app can be installed from the Google Play Store.][playstore] Once you have downloaded the app, either choose "Open" from the Play Store page, or locate the application in your app drawer and launch it from there.

###Choosing Settings
The device you are using may have multiple cameras (such as front and back), as well as multiple resolution modes (sizes of images each camera can capture). _You do not need to calibrate every resolution of every camera,_ though it would be great if you did so. When you launch the app, there should be three vertical dots in the upper right-hand corner, tap this, and then tap "Settings" from the menu that appears.
![The "ARToolKit Camera Calibrator" menu.][menu]
First and foremost, we recommend checking the "Force landscape display" checkbox, as you will be moving the phone around at many angles, and swapping layout is not recommended.

####Choosing Which Resolution(s) to Calibrate
Choosing which resolution(s) to calibrate against can be somewhat difficult. Practically every camera maker uses a different camera module, which in turn has different video modes. *There is no resolution guaranteed to be available on all Android devices. That being said, 320x240 (4:3) is available on most devices.*
![The resolution selections available on a Google Nexus 5.][resolutions]
The good news is that it's not the resolution that matters as much as the aspect ratio. Therefore, we recommend you capture one resolution of each aspect ratio for the camera on your device. The most common standard aspect ratios are 4:3, 3:2, and 16:9. We recommend you calibrate for each of these three aspect ratios, if available.

####Why Calibrate the Front Camera?
Because some AR applications actually make use of the front camera! If your application uses the front camera, or you want to do a good service, we recommend you follow the above resolution recommendations for the front camera also.

####Selecting your Chessboard
![Choosing which chessboard you've printed via the menu.][paper]
If you've downloaded and printed the A4-sized pattern, select "A4". If you've downloaded and printed the US Letter-sized pattern, select "US Letter".

###Capturing Calibration Images
Press the back button (left triangle) to return to the camera feed, and tap the screen in the center box to begin.
![The app upon first launch, instructing you to touch the box to proceed to calibrating.][beginning]
You will be capturing a total of 10 images during this calibration. In the bottom-center of the capture window is displayed the number of images captured so far. *Touching the screen captures an image, so be careful as you reposition yourself. You can always repeat these 10 image captures again if it did not go well the first time.*

[On the left: A good camera capture. On the right: A bad camera capture.][good_bad]
Point the camera at the chessboard grid, and the inner corners of the squares will be highlighted with "X" marks and numbered. Be sure to keep the entire chessboard in view, and hold still during capture.

When the camera can clearly see all the intermediate corners, the X marks turn RED, and a calibration image can be captured- This is good! On the other hand, if some of the corners are obscured by the edges of the camera frame, or poor lighting or reflection, the crosses will be GREEN, and no calibration image can be captured until the optical conditions are changed. This is bad!

In order to obtain a good calibration for the camera, it is important to obtain images of the calibration board at a variety of angles to the camera lens. The images below give examples of the configurations of the calibration board you should try to obtain.
[An example of good framing.][framed1] [Another example of good framing.][framed2]
Capturing these images involves holding the camera at different angles to the board, including upside-down. We do not recommend exceeding an angle of 45 degrees during capture. Do this a total of 10 times.

###Finishing Up
Once you've captured all 10 images, the screen will display "Calculating camera parameters...". Once it has finished it will display your results, like so:
[The results for a calibration captured on a Google Nexus 5.][results]
This screen displays the minimum, maximum, and average error from the frames captured. *In general, having an error threshold below 1.0 is good. If your standard error is above 5 on a non-HD resolution, we recommend you complete the calibration again, being careful with camera focus, chessboard flex, and lighting.*

Congratulations! You've calibrated your camera! We recommend you go and calibrate for the rest of the recommended aspect ratios, listed above.

##What Information is Collected?
If a calibration dataset generated with the app meets a certain minimum level of quality is saved at the completion of calibration, and uploaded when a network connection is available. The calibration file itself contains lens optical and distortion parameters (a structure known as ARParam, if you are familiar with the ARToolKit source).

As well as the calibration file itself, the following information is transmitted:

-   The make and model of device (e.g. Samsung Galaxy S).
-   Which camera on the device the parameters apply to.
-   The date and time at which the calibration file was generated.
-   The calibration data quality (error values).

No personally identifying data is transmitted or stored during as part of the process. Additionally, the data is uploaded via a secure HTTPS connection.

[playstore]:https://play.google.com/store/apps/details?id=com.artoolworks.ar.utils.calib_camera
[patterna4]: http://artoolkit.org/docs/Calibration%20chessboard%20(A4).pdf
[patternus]: http://artoolkit.org/docs/Calibration%20chessboard%20(US%20Letter).pdf
[print_dialog]: :print_dialog.png
[play_store]: :play_store.png
[menu]: :menu.png
[resolutions]: :resolutions.png
[cameras]: :cameras.png
[paper]: :paper.png
[beginning]: :beginning.png
[good_bad]: :good_bad.png
[framed1]: :framed1.png
[framed2]: :framed2.png
[results]: :results.png
