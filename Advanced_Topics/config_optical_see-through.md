# Usng an Optical See-Through Display
Traditionally, applications built on ARToolKit use a video feed on which augmentations are overlaid. ARToolKit also supports using optical see-through displays for augmented reality. Instead of rendering both the background camera feed and the augmentations, the optical see-through display renders the augmentations, and background is the world around you. Examples of higher-end see-though HMDs (head-mounted devices) include the DAQRI Smart Helmet and the Epson Moverio.

If your see-through display is a stereo display (one display for each eye), you are able to render stereoscopically (providing depth) with an optical see-through display, rendering a different perspective for each eye. Regardless of whether you are using a monocular or stereo display, there is the benefit that there is no separation from the real world - You're not looking at the world around you put up on a screen..

Be aware, however, that benefit can also cause issues - There will always be some lag between the augmentations displayed on the optics and the real world passing by behind them. Nowadays, with higher-end devices it is much less noticeable, but older devices will struggle with this lag, or "swimming" effect.

For a full discussion of the advantages and disadvantages of optical and video see-through AR, you can refer to [Ron Azuma's course notes on Augmented Reality][1].

##Registration
For the most accurate registration, that is, alignment between your eyes, the augmentations, and the world, it is necessary to know the position of the user's eyes relative to the display optics, and the camera which tracks the world. With ARToolKit, this is achieved by a simple self-calibration method in which the user holds a calibration pattern in front of the eye and lines up the pattern with a virtual cross hair shown in the see-through display. In an ideal world, the eye position calibration should be done each time a user starts the AR application, especially if it is a different user.

##Calibration
Before calibrating the displays themselves, you must first [calibrate your camera][2]. This is extra important when using a stereo display as any registration error (any offset in position between the real world object and its viewed position in the display) will be much more obvious when viewing stereoscopically, and will normally be perceived as the depth of the augmentation being incorrect.

###calib_optical
The calib_optical utility is used to calibrate the displays tot he camera position. Calibration is done monocularly (one eye, one perspective at a time), and as such should be conducted for each eye in turn (run first for one eye with the other closed, and then vice-versa). You will use spacebar when required for most configuration actions. It is used as follows:

1.  With the HMD placed firmly on your head, run the calib_optical application.
2.  Press the space bar. A white crosshair should appear on-screen.
3.  Looking only through the eye being calibrated (i.e. with the other closed or covered), view calibration card roughly at arms length. ![A user performing optical calibration by lining up their eye position with the pattern][performing_optical_calibration]
4.  Move the calibration card until a red or green square appears at the intersection of the white cross hairs. This means that the calibration card is in view of the head mounted camera and it’s pattern has been recognized.
5.  Keeping the unused eye shut and the red or green square active move the calibration card and move your head to line up the white cross hairs with the intersection of the squares on the card. ![View in headset during optical calibration procedure][optical_calibration_view]
6.  Press the space bar once the crosshairs are aligned with the squares' intersection. If the calibration parameters are captured the red or green square will change to the opposite color.
7.  Keeping the unused eye shut, move the calibration card as close as possible to your viewpoint while keeping the red or green square active and repeat steps 5 and 6.
8.  After capturing a calibration point at arms length and close to the body, the cross hairs should change position – keeping your right eye shut repeat steps 3 through 7. There are 5 calibration positions so ten measurements are taken in total for one eye.

If at any point you need to see the video-image (temporarily, e.g. to see if the camera is correctly focussed or has correct brightness or contrast) press the "o" key. While in this mode, you can press "d" to see the debug (binarized image) and "-" and "+" to adjust the binarization threshhold to get nice black and white borders on the pattern.

After taking ten measurements, the white cross hairs will disappear and the calibrated eye position will be printed out, looking something like this:
<pre>
    ./calib_opticalCamera image size (x,y) = (640,480)
    Reading camera parameters from Data/camera_para.dat (distortion function version 3).
    *** Camera Parameter ***
    --------------------------------------
    SIZE = 640, 480
    Distortion factor = 311.500000 226.000000 1.006924 1.000000 11.000000 4.400000
    804.38635 0.00000 312.50000 0.00000
    0.00000 803.87536 239.00000 0.00000
    0.00000 0.00000 1.00000 0.00000
    --------------------------------------
    ProcMode (X)   : FRAME IMAGE
    DrawMode (C)   : TEXTURE MAPPING (FULL RESOLUTION)
    TemplateMatchingMode (M)   : Color Template
    Window was resized to 640x480. Camera image of 640x480 will be scaled by 1.000000 (h) and 1.000000 (v).
    CTYPE = 2vuy
    Beginning optical see-through calibration.
    Position 1 (far) captured.
    -- 3D position -115.184635, 57.446030, 564.060060.
    -- 2D position 160.000000, 120.000000.
    Position 1 (near) captured.
    -- 3D position -103.269729, 60.947248, 410.983793.
    -- 2D position 160.000000, 120.000000.
    Position 2 (far) captured.
    -- 3D position 55.854849, 60.853172, 547.750355.
    -- 2D position 480.000000, 120.000000.
    Position 2 (near) captured.
    -- 3D position 21.727804, 60.089365, 391.802531.
    -- 2D position 480.000000, 120.000000.
    Position 3 (far) captured.
    -- 3D position -27.638938, -10.452357, 562.451288.
    -- 2D position 320.000000, 240.000000.
    Position 3 (near) captured.
    -- 3D position -48.164517, 28.288982, 297.542144.
    -- 2D position 320.000000, 240.000000.
    Position 4 (far) captured.
    -- 3D position -110.804220, -80.708711, 567.940307.
    -- 2D position 160.000000, 360.000000.
    Position 4 (near) captured.
    -- 3D position -96.756636, -22.429633, 361.695711.
    -- 2D position 160.000000, 360.000000.
    Position 5 (far) captured.
    -- 3D position 61.444556, -77.380158, 556.955252.
    -- 2D position 480.000000, 360.000000.
    Position 5 (near) captured.
    -- 3D position 42.332470, -56.220412, 461.777917.
    -- 2D position 480.000000, 360.000000.
    Expressed relative to camera axes, eye is -70.561950 mm to the right, -70.495486 mm above, and 30.678455 mm behind the camera.
    Eyepoint error is 124.106253.
    --------------------------------------
    Field-of-view vertical, horizontal = 27.056970, 32.055244 degrees, aspect ratio = 1.184731
    Transformation (eye to camera) =
    0.98718 -0.14631 0.05781 -70.56195
    0.15453 0.96684 -0.11723 -70.49549
    -0.03987 0.12466 0.97706 30.67845
    0.00000 0.00000 0.00000 1.00000
    --------------------------------------
    Optical display parameters and eye to camera transformation matrix saved to file optical_param.dat.
</pre>

You will note that a measurement of the calibration error is generated. The lower this value, the more accurate the calibration.

At this point you will be prompted for the name of the file in which to save the calibration results. If you are calibrating a stereo display, switch eyes and repeat steps 3 through 8 to capture ten measurements for the other eye. Although the calibration process may appear quite time consuming, with practice it can be completed in just a couple of minutes and should produce good optical viewing results.

###Testing Calibration
The [applications for monocular and stereo optical displays][example_optical] are examples for desktop demonstrating optical see-through with a calibrated camera and display. These applications are a good way to test your optical configuration(s), completed above.

##Using the Calibration Files

###Desktop
You will want to move the newly-generated calibration files into the `Data/` directory of your application.

###Unity
The ARToolKit Unity plugin supports both monocular and stereo see-through rendering out-of-the-box. For stereo, only half-width side-by-side stereo mode is supported currently, as used in e.g. the Epson Moverio BT-200 display.

To use the optical calibration results in ARToolKit for Unity, the parameters file must be renamed and moved into the correct location inside your Unity project. The correct location is inside a folder at path `Assets/Resources/ardata/optical` inside your Unity project. Unlike on other platforms or renderers, the file name must end with the suffix ".bytes" for Unity to recognize it. E.g. If your parameters file is named "optical_param.dat", rename it to "optical_param.bytes" and drop it into this folder. The first part of the filename can be named to help you identify the parameters.

![ARToolkit for Unity optical parameters file location.][ARToolKit_for_Unity_optical_parameters_file_location]

Once the parameters file is in this location, optical mode should be enabled in the "ARCamera" component in your Unity project. A popup will show a list of all available ".bytes" files in the `Assets/Resources/ardata/optical` folder. Select the preferred parameters file.

![ARToolKit for Unity optical mode enabled.][ARToolKit_for_Unity_optical_mode_enabled]

By default, when using optical mode, the video background is initially turned off. If you want to see the video image, press *Enter* (desktop platforms) or *Menu* (Android) and use the on-screen control to toggle the video background on or off. This, of course, can be changed by modifying the scripts.

####Converting to Stereo
Stereo optical see-through is set up in Unity by taking an existing Camera object with an ARCamera script attached, and duplicating it (in the Unity Editor, select the Camera game object, then choose "Edit-\>Duplicate" from the menu bar). You can rename the cameras to make clear which camera corresponds to which eye, as in this example:

![ARToolKit for Unity stereo optical camera][ARToolKit_for_Unity_stereo_optical_cameraL.png]

On each camera, tick the boxes “Part of a stereo pair” and “Optical see-through mode”. On the desired “left” camera, choose “Stereo eye: left” and select the calibrated optical parameters file for the left eye from the "Optical parameters file" popup. Repeat step 4 for the right eye.

####Alternative Stereo Configuration
The Unity plugin also supports an alternative configuration for stereo optical- Optical calibration is instead performed only for one eye, and then this value is used for both eyes with a manual "offset" value applied to the second eye. This arrangement is better when the distance between the eyes can be accurately estimated. You might wish to use the [adult-population average][interpupillary_distance] eye separation of 0.065 metres (65 millimetres, or 2.56 inches).

To set up in this way, set up as above, but choose the same "Optical parameters file" popup for both left and right eyes. Then, if the optical calibration is for the right eye, enter a negative value in the box labelled "Lateral offset right" for the left eye camera, e.g. -0.065. If the optical calibration file is for the left eye, enter a positive value in the box for the right eye camera, e.g. 0.065.

##Limitations
While optical see-through AR is an attractive ideal, in practice it is very difficult to achieve accurate registration with optical see-through AR systems. (Registration is the alignment of the virtual objects shown in the display and their real-world referent). Most of these limitations come from the properties of the display itself, not the calibration procedures.

Optical see-through calibration depends on accurately knowing the precise relationship of two optical apertures: the iris of the camera imaging the scene, and the iris of the eye of the user viewing the scene. We can estimate the relationship between the two by measuring the distance between the display being used to produce the imagery and the lens of the camera, but the position of the iris of the eye of the user and the display is not fixed. We can attempt to control this relationship by fixing the display very tightly in place on the user's head, but its position will differ by small amounts between sessions and between users. Even when accurate calibration has been achieved, a tiny shift in the position of the display relative to the user's eye can produce a significant offset in registration of objects in the scene. Unless using a headset which includes eye-tracking, accuracy of registration is limited.

Of course, alignment between virtual and real objects is desirable for video see-through too, but in video see-through the users sees the virtual objects overlaid on the source image being used for tracking. There is minimal registration error between the video stream and the overlaid objects, and the misalignment of the video stream and the real scene behind and around it is much less noticeable to the user. This is one of the key reasons why video see-through display has become so widely used in AR research.

[1]: http://www.cs.unc.edu/~azuma/azuma_AR.html
[2]: Configuration:config_camera_calibration
[example_optical]: Examples:example_optical
[interpupillary_distance]: https://en.wikipedia.org/wiki/Interpupillary_distance

[optical_calibration_pattern]: /Optical_calibration_pattern.png
[performing_optical_calibration]: /Performing_optical_calibration.png
[optical_calibration_view]: /Optical_calibration_view.png
[ARToolKit_for_Unity_optical_parameters_file_location]: /ARToolKit_for_Unity_optical_parameters_file_location.png
[ARToolKit_for_Unity_optical_mode_enabled]: /ARToolKit_for_Unity_optical_mode_enabled.png
[ARToolKit_for_Unity_stereo_optical_cameraL]: /ARToolKit_for_Unity_stereo_optical_cameraL.png