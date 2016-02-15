#NFT Utilities for ARToolKit
This page is a description of the tools used along with [NFT tracking][marker_nft_training].

##checkResolution
The checkResolution tool supplied with ARToolKit can help in determining the required resolution of source image data used in creating an NFT dataset.

###Operational summary

1.  Obtain the NFT image to be tracked in printed form. ![Pinball NFT Sample][Pinball_NFT_sample_printed_with_hand]
2.  Print a single standard ARToolKit "Hiro" marker and trim excess paper around the outside. The Hiro marker can be printed at any size; 40 mm is a good size (approximately 2 inches). ![Hire marker on paddle][Hiro_marker_on_paddle_40mm]
3.  Connect your camera and run from a terminal / command prompt.
    -   Mac OS X/Linux: `./checkResolution`
    -   Windows: `checkResolution.exe

You will be prompted to enter the size of the Hiro marker. E.g. if printed at 40 mm size, enter `40`.

-   The camera is pointed towards the printed image to be tracked, and the Hiro marker is positioned so that it is on top of the other marker, positioned in the middle of the camera frame. The display indicates the tracked marker in green, with a red cross at the centre of the marker, and below, the vertical and horizontal resolution of the printed image directly under that point.
![This screen shot displays the output when the camera is at a typical user distance - image resolution is around 50 dpi.][CheckResolution_pinball_marker_mid-distance]

-   The camera is moved around (with the Hiro marker moved each time so that it remains roughly in the centre of the camera frame) to the maximum and minimum distances the tracked marker is likely to be seen from:
![This screen shot displays the output when the camera has been moved as close as likely to be required to the tracked image - image resolution is around 150 dpi][CheckResolution_pinball_marker_close-distance]
![This screen shot displays the output when the camera has been moved as far away from the tracked image as likely to be required in normal use - image resolution is around 25 dpi][CheckResolution_pinball_marker_far-distance]

### Using the Output
Moving the camera around and observing the DPI values should give you an idea of the [maximum resolution][marker_nft_training] required when producing the digital version of the printed material to be tracked (it is not recommended to produce imagery at a higher resolution than the printed version, which is typically 150dpi). Additionally, the output helps determine the range of resolutions required when running the genImageSet tool as the first step in training a new NFT data set.

###Tips for Best Use
Be sure to use a camera running at the same frame size as will be used in the online tracking process; the DPI values produced depend on the camera image size. In spite of megapixel webcams being the norm, it is actually better to use a lower resolution camera with a higher frame rate; 640x480 is perfectly adequate for most NFT tracking situations.

###Keyboard / Mouse Controls
Below is a table of keyboard / mouse controls for using checkResolution:

| Key | Function                         |
|-----|----------------------------------|
| esc | Quit program                     |
| 1   | Decrease binarization threshold  |
| 2   | Increase binarization threshold. |

##dispFeatureSet
dispFeatureSet displays trained NFT datasets by overlaying representations of the data points on the source images.

Usage:

<pre>
    ./dispFeatureSet <filename>
      -fset     Show fset features.
      -fset3    Show fset3 features.
</pre>

After launching dispFeatureSet, the various image resolutions will be displayed on screen with the tracking features overlaid. The features used in continuous tracking are outlined by red boxes, and the features used in identifying the pages and initializing tracking are marked by green crosses.

![ARToolKit NFT - dispFeatureSet terminal][ARToolKit_NFT_-_dispFeatureSet_terminal]
![ARToolKit NFT - dispFeatureSet][ARToolKit_NFT_-_dispFeatureSet]

##dispImageSet
dispImageSet displays compressed image pyramids.

Usage:
<pre>
    ./dispImageSet <filename>
</pre>

After launching dispImageSet, the various image resolutions will be displayed on screen (shrunk/zoomed as necessary to fit on screen). Press spacebar to view the images, or esc when you're done.

![ARToolKit NFT - dispImageSet terminal][ARToolKit_NFT_-_dispImageSet_terminal]
![ARToolKit NFT - dispImageSet][ARToolKit_NFT_-_dispImageSet]

##genTexData
genTexData performs training of NFT datasets from a supplied JPEG-format source image.

Usage:
<pre>
    ./genTexData <filename>
        -level=n
             (n is an integer in range 0 (few) to 4 (many). Default 2.'
        -sd_thresh=<sd_thresh>
        -max_thresh=<max_thresh>
        -min_thresh=<min_thresh>
        -leveli=n
             (n is an integer in range 0 (few) to 3 (many). Default 1.'
        -feature_density=<feature_density>
        -dpi=<dpi>
        -max_dpi=<max_dpi>
        -min_dpi=<min_dpi>
        -background
             Run in background, i.e. as daemon detached from controlling terminal. (Mac OS X and Linux only.)
        -log=<path>
        -loglevel=x
             x is one of: DEBUG, INFO, WARN, ERROR. Default is INFO.
        -exitcode=<path>
        --help -h -?  Display this help
</pre>

## Operating Example
Exit codes:
<pre>
E_NO_ERROR = 0
E_BAD_PARAMETER = 64
E_INPUT_DATA_ERROR = 65
E_USER_INPUT_CANCELLED = 66
E_BACKGROUND_OPERATION_UNSUPPORTED = 69
E_DATA_PROCESSING_ERROR = 70
E_UNABLE_TO_DETACH_FROM_CONTROLLING_TERMINAL = 71
E_GENERIC_ERROR = 255
</pre>

See [Training NFT to a new surface][marker_nft_training] for more information on NFT datasets.

[marker_nft_training]: 3_Marker_Training:marker_nft_training
[Pinball_NFT_sample_printed_with_hand]: :pinball_nft_sample_printed_with_hand.jpg
[Hiro_marker_on_paddle_40mm]: :hiro_marker_on_paddle_40mm.jpg
[CheckResolution_pinball_marker_mid-distance]: :checkresolution_pinball_marker_mid-distance.png
[CheckResolution_pinball_marker_close-distance]: :checkresolution_pinball_marker_close-distance.png
[CheckResolution_pinball_marker_far-distance]: :checkresolution_pinball_marker_far-distance.png
[ARToolKit_NFT_-_dispFeatureSet_terminal]: :artoolkit_nft_-_dispfeatureset_terminal.png
[ARToolKit_NFT_-_dispFeatureSet]: :artoolkit_nft_-_dispfeatureset.png

[ARToolKit_NFT_-_dispImageSet_terminal]: :artoolkit_nft_-_dispimageset_terminal.png
[ARToolKit_NFT_-_dispImageSet]: :artoolkit_nft_-_dispimageset.png
