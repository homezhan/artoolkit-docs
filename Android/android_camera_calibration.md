#Camera Calibration App for Android
This application allows you to generate calibration parameters for the lens on your Android device. Good quality lens calibration can be used to improve ARToolKit tracking on your device.

After capture, lens calibration data that meets a certain minimum level of quality is saved on ARToolworks lens calibration data server, and may be shared with other users of the same model of device.

##Requirements

-   The application requires Android v2.2 or later.
-   A printer is required to print the calibration pattern.
-   A network connection (e.g. wifi or cellular data) is required to upload the data. Without this, the app does not serve any useful purpose.

##How it Works
The [calibration pattern][chessboard] consists of a grid of black and white squares surrounded by a white border. When viewed through the camera lens, lens distortion causes the straight lines at the edges of the squares to appear curved. The calib_camera program uses the OpenCV library to locate the corners of the squares and then measures the spacing between the corners and uses this information to calculate the lens distortion. The more images captured, and the more angles they are captured from, the lower the error in the distortion measurement.

Download the calibration chessboard [here][chessboard].

##How do I use it?

### Setting up
Calibration works by capturing images of the pre-prepared calibration pattern with the camera. The calibration pattern can be printed from the app (via Google Cloud Print service) by selecting the "Print" button from app. To access the Print button, press the hardware menu button on the device or use the menu button on the Action Bar at the top of the screen (on Android devices without a hardware menu button).

![Chessboard pattern affixed to board ready for calibration][chessboard_screen]
Once printed, the pattern must be affixed to a flat surface. The easiest means of doing this is to use a piece of thin very flat board (as might be obtained from a hardware store) and a dry glue. Using a millimeter rule, measure the size of the edges of the squares. If printed without scaling, this distance will be exactly 30 mm. Other sizes can be used, as long as they are accurately known.

Finally, set up your camera. A calibration file is only valid for one focus setting of the camera (although it will still work at other focal lengths), so choose in advance the focus setting for the camera which will be used most often.

[Click here to read detailed directions on the calibration procedure for ARToolKit for Desktop][calibrating_camera]

1.   Before beginning, print out the calibration chessboard pattern and affix it to a flat surface. See the [setup][calibrating_camera] documentation for more information.
2.   After launching the app, you can use the Settings menu to choose the camera and resolution to be calibrated. To access the Settings menu, press the hardware menu button on the device or use the menu button on the Action Bar at the top of the screen (on Android devices without a hardware menu button).
3.   Collect calibration images. See [capturing calibration images][calibrating_camera] for more information.
4.   Once all images have been collected, the calibration data will be calculated, and when this is complete the results will be shown on-screen.
5.   The calibration data is automatically uploaded.

##What Information is Collected?
If a calibration dataset generated with the app meets a certain minimum level of quality is saved at the completion of calibration, and uploaded when a network connection is available. The calibration file itself contains lens optical and distortion parameters (basically an ARParam structure).

As well as the calibration file itself, the following information is transmitted:

-   The make and model of device (e.g. Samsung Galaxy S).
-   Which camera on the device the parameters apply to.
-   The date and time at which the calibration file was generated.
-   The calibration data quality (error values).

No personally identifying data is transmitted or stored during as part of the process. Additionally, the data is uploaded via a secure HTTPS connection.

[chessboard]:/File:Calibration_chessboard.pdf "wikilink"
[chessboard_screen]: :chessboard_ready_for_calibration_1.jpg
[calibrating_camera]: Configuration:config_camera_calibration "wikilink"
