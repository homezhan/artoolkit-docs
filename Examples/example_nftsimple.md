#nftSimple - NFT Example

##About nftSimple
nftSimple is an application that demonstrates the NFT tracking alongside very simple rendering. When an NFT surface is recognized, the familiar colorcube (also seen in the simpleLite example) will be drawn at the origin of the dataset's coordinate system.

For developers who are already familiar with the code of simpleLite, it will be useful to do a side-by-side comparison of the code of nftSimple. The basic flow of program operations (grab a frame, track markers, render) is very similar, however there are significant changes in how the marker information is handled, as well as the control flow in the tracking loop.

The NFT data set loaded by nftSimple is specified in the file "bin/Data2/markers.dat". This is a simple text file that specifies the number of markers, their type, and the path to their data. As supplied, this file points to the sample "pinball" dataset (an image of a pinball play surface), provided in ARToolKit/bin/DataNFT. This directory contains the required image set and feature sets. The original image to be printed is in a different directory, ARToolKit/doc/patterns.

##Preparation

-   Print out the jpeg file doc/patterns/pinball.jpg on a color printer.

The image is 1637 pixels wide and 2048 pixels high, with a resolution of 220 dots per inch (dpi). When printed at 1:1 scaling, its printed size should be 189.0 mm wide and 236.5 mm tall. This should fit comfortably onto a single sheet of A4 paper (210 mm x 297 mm) or US Letter paper (215.9 mm × 279.4 mm).

If instead you wish to print the image on smaller paper, the image can either be cropped top and bottom, or scaled to fit. Cropping will maintain correct distance measurements in ARToolKit, at the cost of perhaps losing some of the tracking points, whereas scaling will result in measurements returned by ARToolKit being scaled by the same amount.

-   Connect your webcam.
-   Work out any webcam configuration required. Generally, if your webcam produces images greater than 800x600 resolution, it is recommended to either use the dialog box (where applicable) or set an ARToolKit video configuration environment variable to choose a resolution no greater than 800x600. A resolution of 640x480 is perfectly acceptable for NFT, and the greater frame rate achievable by using this resolution rather than a higher resolution is of more advantage than a larger frame size. See [Configuring Video Capture in ARToolKit][1] for details on this.
-   Carefully [calibrate your camera][2]) and copy the calibration data into the ARToolKit/bin/Data2 directory, overwriting the file camera\_para.dat

##Launch nftSimple
Windows/Mac OS X: Double click the "nftSimple" application in ARToolKit's "bin" directory. Linux: From a terminal, cd to `ARToolKit/bin` and type: `./nftSimple`.

##Operation
Once the application is running, point the camera at the image.

![KPM example][NFT_example_KPM_holding_webcam]

The tracking should rapidly pick up the image. Once the image is recognized, the colorcube will be drawn at the origin of the page's coordinate system.

[1]: Configuration:config_video_capture
[2]: Configuration:config_camera_calibration

[NFT_example_KPM_holding_webcam]: :nft_example_kpm_holding_webcam_1.jpg
