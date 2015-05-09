# ARToolkit Documentation
ARToolKit is software that lets programmers easily develop Augmented Reality applications. Augmented Reality (AR) is the embedding of computer generated content into the natural environment, and has many potential applications in entertainment, media, advertising, industry, and academic research.

One of the most difficult parts of developing an augmented reality application is precisely calculating the user's viewpoint in real time so that the virtual images are exactly aligned with real world objects. ARToolKit uses computer vision techniques to calculate the real camera position and orientation relative to square shapes or flat textured surfaces, allowing the programmer to overlay virtual objects. ARToolKit currently supports classical square marker, 2D barcode, multimarker, and natural feature tracking. Furthermore, ARToolKit supports any combination of the above together. The fast, precise tracking provided by ARToolKit has enabled the rapid development of thousands of new and interesting AR applications.

The documentation contains a complete description of the ARToolKit library, how to install it, and how to use its functionality in AR applications. Several simple sample applications are provided with ARToolKit to enable the programmer to get started immediately. ARToolKit includes the tracking libraries and complete source code for these libraries enabling programming to port the code to a variety of platforms or customize it for their own applications.

ARToolKit is multi-platform, running on the Windows, Mac OS X, Linux, iOS and Android operating systems. The functionality of each version of the toolkit is the same, but the performance may vary depending on the different hardware configurations. ARToolKit can be easily ported to other new and experimental platforms.

ARToolKit supports both video and optical see-through augmented reality. Video see-through AR is where virtual images are overlaid on live video of the real world. The alternative is optical see-through augmented reality, where computer graphics are overlaid directly on a view of the real world. Optical see-through augmented reality typically requires a see-through head mounted display and has more complicated camera calibration and registration requirements.

##Introduction
-   [ARToolKit Feature Comparison][3]
-   [Installing ARToolKit][4]
-   [Introduction to Template Markers][]
-   [Introduction to Natrual Feature Markers][]
-   [Frequently Asked Questions][about_faq]

##Getting Started
-   [Tutorial: Hello, World! First simple ARToolKit scene.][5]

##Configuring ARToolKit
-   [Setting up a Video Capture Device][config_video_capture]
-   [Calibrating your Camera][camera_calibration]

##Marker Types, Training and Usage
-   [Markers][marker_training]
-   [2D-Barcode Markers][marker_barcode]
-   [Multimarkers][marker_multi]
-   [NFT Markers][nft_training]
-   [Troubleshooting Marker Recognition Issues][marker_troubleshooting]

##Using NFT Markers
-   [ARToolKit NFT Utilities][35]
-   [Running the nftSimple example][32]
-   [Graphics, models, and advanced rendering][9]

##Advanced Topics
-   [Using an Optical See-Through Display][config_advanced_optical_see-through]
-   [Configuring ARToolKit for Stereo Tracking][camera_advanced_stereo_tracking]
-   [Adjusting ARToolKit for lighting conditions][camera_adjusting_for_lighting]
-   [Building libARvideo on Windows][windows_building_libarvideo]
-   [Hardware Selection][about_hardware_selection]
-   [Building from Source][build_artoolkit]
-   [Customising the ToolKit][about_customising]

##General Topics
-   [Setting an Environment Variable][general_environment_variables]
-   [Deploying an Application on Windows/OS X][general_deploy_application]

##Related Documentation (Off-Site)
-   [ARToolKit v2.x documentation][external_2x_docs]
-   [Inside ARToolKit][external_inside_artoolkit] Tutorial given at ART 02 by Hirokazu Kato
-   [Marker Tracking and HMD Calibration for a Video-Based Augmented Reality Conferencing System][external_hmd_conferencing] by Hirokazu Kato and Mark Billinghurst.
-   [A Registration Method based on Texture Tracking using ARToolKit][external_registration_method] by Hirokazu Kato, Keihachiro Tachibana, Mark Billinghurst, and Michael Grafe.

[external_2x_docs]: http://www.hitl.washington.edu/artoolkit/documentation/
[external_inside_artoolkit]: http://www.hitl.washington.edu/artoolkit/Papers/ART02-Tutorial.pdf
[external_hmd_conferencing]: http://www.hitl.washington.edu/artoolkit/Papers/IWAR99.kato.pdf
[external_registration_method]: http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=1320435