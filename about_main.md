# ARToolkit Documentation
ARToolKit is software that lets programmers easily develop Augmented Reality applications. Augmented Reality (AR) is the embedding of computer generated content into the natural environment, and has many potential applications in entertainment, media, advertising, industry, and academic research.

One of the most difficult parts of developing an augmented reality application is precisely calculating the user's viewpoint in real time so that the virtual images are exactly aligned with real world objects. ARToolKit uses computer vision techniques to calculate the real camera position and orientation relative to square shapes or flat textured surfaces, allowing the programmer to overlay virtual objects. ARToolKit currently supports classical square marker, 2D barcode, multimarker, and natural feature tracking. Furthermore, ARToolKit supports any combination of the above together. The fast, precise tracking provided by ARToolKit has enabled the rapid development of thousands of new and interesting AR applications.

The documentation contains a complete description of the ARToolKit library, how to install it, and how to use its functionality in AR applications. Several simple sample applications are provided with ARToolKit to enable the programmer to get started immediately. ARToolKit includes the tracking libraries and complete source code for these libraries enabling programming to port the code to a variety of platforms or customize it for their own applications.

ARToolKit is multi-platform, running on the Windows, Mac OS X, Linux, iOS and Android operating systems. The functionality of each version of the toolkit is the same, but the performance may vary depending on the different hardware configurations. ARToolKit can be easily ported to other new and experimental platforms.

ARToolKit supports both video and optical see-through augmented reality. Video see-through AR is where virtual images are overlaid on live video of the real world. The alternative is optical see-through augmented reality, where computer graphics are overlaid directly on a view of the real world. Optical see-through augmented reality typically requires a see-through head mounted display and has more complicated camera calibration and registration requirements.

##Introduction

-   [How ARToolKit works][2]
-   [ARToolKit feature comparison][3]
-   [Installing ARToolKit][4]
-   [Frequently Asked Questions][about_faq]
-   [Tutorial: Hello, World! First simple ARToolKit scene.][5]

###Further Reading
-   [Hardware Selection][about_hardware]
-   [Building from Source][build_artoolkit]
-   [Customising the ToolKit][about_customising]
-   [Deploying for Windows / OS X][]


##Configuring ARToolKit
-   [Setting Environmental Variables][config_evnironment_variables]
-   [Setting up a Video Capture Device][config_video_capture]
-   [Calibrating your Camera][camera_calibration]
-   []
-   []

###Advanced Configuration
-   [Using an Optical See-Through Display][config_advanced_optical_see-through]
-   [Configuring ARToolKit for Stereo Tracking][camera_advanced_stereo_tracking]
-   [Adjusting ARToolKit for lighting conditions][camera_adjusting_for_lighting]
-   [Building libARvideo on Windows][windows_building_libarvideo]

##Marker Types
-   [Markers][marker_training]
-   [2D-Barcode Markers][marker_barcode]
-   [Multimarkers][marker_multi]
-   [NFT Markers][nft_training]

###Advanced Marker Topics
-   [Troubleshooting Marker Recognition Issues][marker_troubleshooting]

##Using NFT Markers
-   [ARToolKit NFT Utilities][35]
-   [Running the nftSimple example][32]
-   [Graphics, models, and advanced rendering][9]

###Related Documentation (Off-Site)
-   [ARToolKit v2.x documentation][28]
-   [Inside ARToolKit][29]* (Tutorial given at ART 02 by Hirokazu Kato)
-   [Marker Tracking and HMD Calibration for a Video-Based Augmented Reality Conferencing System][30] by Hirokazu Kato and Mark Billinghurst.
-   [A Registration Method based on Texture Tracking using ARToolKit][40] by Hirokazu Kato, Keihachiro Tachibana, Mark Billinghurst, and Michael Grafe.

[1]: /About_ARToolKit
[2]: /How_ARToolKit_works
[3]: /ARToolKit_feature_comparison
[4]: /Installing_ARToolKit_Professional
[5]: /ARToolKit_tutorial_1:_First_simple_ARToolKit_scene
[6]: /Calibrating_your_camera
[7]: /Creating_and_training_new_ARToolKit_markers
[8]: /Using_an_optical_see-through_display
[9]: /Graphics,_models,_and_advanced_rendering
[10]: /Using_2D-barcode_markers
[11]: /Multimarker_tracking
[12]: /Adjusting_ARToolKit_for_lighting_conditions
[13]: /Converting_to_ARToolKit_4_-_Part_1_-_simpleLite.pdf
[14]: /Configuring_video_capture_in_ARToolKit_Professional
[15]: /Hardware_selection_and_configuration_for_ARToolKit
[16]: /Building_ARToolKit_Professional_from_source
[17]: /Customising_other_aspects_of_ARToolKit
[18]: /ARToolKit_FAQs
[19]: /Debugging_marker_recognition_problems
[20]: /Using_stereo_tracking
[21]: /Deploying_an_application_using_ARToolKit_Professional
[22]: /ARToolKit_for_iOS
[23]: /ARToolKit_for_Android
[24]: http://www.artoolworks.com/support/doc/artoolkit5/apiref/masterTOC.html
[25]: http://www.artoolworks.com/support/doc/artoolkit5/apiref-ARWrapper/html/index.html
[26]: http://artoolkit.sourceforge.net/apidoc/
[27]: /ARToolKit_Professional_Release_Notes
[28]: http://www.hitl.washington.edu/artoolkit/documentation/
[29]: http://www.hitl.washington.edu/artoolkit/Papers/ART02-Tutorial.pdf
[30]: http://www.hitl.washington.edu/artoolkit/Papers/IWAR99.kato.pdf
[31]: /About_ARToolKit_NFT
[32]: /Running_the_nftSimple_example
[33]: /Training_ARToolKit_NFT_to_a_new_surface
[34]: /Using_ARToolKit_NFT_with_fiducial_markers
[35]: /ARToolKit_NFT_Utilities:_checkResolution
[36]: /ARToolKit_NFT_Utilities:_genTexData
[37]: /ARToolKit_NFT_Utilities:_dispImageSet
[38]: /ARToolKit_NFT_Utilities:_dispFeatureSet
[39]: /ARToolKit_NFT_Release_Notes
[40]: http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=1320435