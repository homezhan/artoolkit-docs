#NFT Utilities in ARToolKit

##checkResolution
The checkResolution tool supplied with ARToolKit NFT can help in determining the required resolution of source image data used in creating an NFT dataset.

### Operational summary

1.  Obtain the NFT image to be tracked in printed form. ![Pinball NFT Sample][Pinball_NFT_sample_printed_with_hand]
2.  Print a single standard ARToolKit "Hiro" marker and trim excess paper around the outside. The Hiro marker can be printed at any size; 40 mm is a good size (approximately 2 inches). ![Hire marker on paddle][Hiro_marker_on_paddle_40mm]
3.  Connect your camera and run from a command prompt.
    -   Windows:
       <pre>checkResolution.exe</pre>
    -   Mac OS X/Linux:
        <pre>./checkResolution</pre>

You will be prompted to enter the size of the Hiro marker. E.g. if printed at 40 mm size, enter **40**.

- The camera is pointed towards the printed image to be tracked, and the Hiro marker is positioned so that it is on top of the other marker, positioned in the middle of the camera frame. The display indicates the tracked marker in green, with a red cross at the centre of the marker, and below, the vertical and horizontal resolution of the printed image directly under that point.
![This screen shot displays the output when the camera is at a typical user distance - image resolution is around 50 dpi][CheckResolution_pinball_marker_mid-distance]
- The camera is moved around (with the Hiro marker moved each time so that it remains roughly in the centre of the camera frame) including to the maximum and minimum distances the tracked marker is likely to be seen from:
![This screen shot displays the output when the camera has been moved as close as likely to be required to the tracked image - image resolution is around 150 dpi][CheckResolution_pinball_marker_close-distance]
![This screen shot displays the output when the camera has been moved as far away from the tracked image as likely to be required in normal use - image resolution is around 25 dpi][CheckResolution_pinball_marker_far-distance]

### Using the output

Moving the camera around and observing the DPI values should give you an idea of the maximum resolution required when producing the digital version of the printed material to be tracked (although as mentioned [here][1], it is not recommended to produce imagery at a higher resolution than the printed version, which is typically 150dpi). Additionally, the output helps determine the range of resolutions required when running the genImageSet tool as the first step in training a new NFT data set.

### Solving problems

Be sure to use a camera running at the same frame size as will be used in the online tracking process; the DPI values produced depend on the camera image size. In spite of megapixel webcams being the norm, it is actually better to use a lower resolution camera with a higher frame rate; 640x480 is perfectly adequate for most NFT tracking situations.

### Keyboard / mouse controls

<table rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;" border="2" cellpadding="3" cellspacing="4">
<tbody><tr>
<th>Key </th><th> Function
</th></tr>
<tr>
<td> esc
</td><td> Quit program
</td></tr>
<tr>
<td> 1
</td><td> Decrease binarization threshold
</td></tr>
<tr>
<td> 2
</td><td> Increase binarization threshold.
</td></tr></tbody></table>

##dispFeatureSet
dispFeatureSet displays trained NFT datasets by overlaying representations of the data points on the source images.

###Usage

<pre>
./dispFeatureSet <filename>
 -fset     Show fset features.
 -fset2    Show fset2 features.
</pre>

After launching dispFeatureSet, the various image resolutions will be displayed on screen with the tracking features overlaid. The features used in continuous tracking are outlined by red boxes, and the features used in identifying the pages and initialising tracking are marked by green crosses.

![ARToolKit NFT - dispFeatureSet terminal][ARToolKit_NFT_-_dispFeatureSet_terminal]
![ARToolKit NFT - dispFeatureSet][ARToolKit_NFT_-_dispFeatureSet]

##dispImageSet
dispImageSet displays compressed image pyramids.

### Usage

<pre>
./dispImageSet <filename>
</pre>

After launching dispImageSet, the various image resolutions will be displayed on screen (shrunk/zoomed as necessary to fit on screen). Press spacebar to view the images, or esc when you're done.

![ARToolKit NFT - dispImageSet terminal][ARToolKit_NFT_-_dispImageSet_terminal]
![ARToolKit NFT - dispImageSet][ARToolKit_NFT_-_dispImageSet]

##genTexData
genTexData performs training of NFT datasets from a supplied JPEG-format source image.

### Usage

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

## Operating example

### Exit codes
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

See [Training ARToolKit NFT to a new surface][2]

[1]: /Training_ARToolKit_NFT_to_a_new_surface#Decide_on_the_image_set_resolutions
[2]: /Training_ARToolKit_NFT_to_a_new_surface

[Pinball_NFT_sample_printed_with_hand]: /Pinball_NFT_sample_printed_with_hand.JPG
[Hiro_marker_on_paddle_40mm]: /Hiro_marker_on_paddle_40mm.jpg 
[CheckResolution_pinball_marker_mid-distance]: /CheckResolution_pinball_marker_mid-distance.png
[CheckResolution_pinball_marker_close-distance]: /CheckResolution_pinball_marker_close-distance.png
[CheckResolution_pinball_marker_far-distance]: /CheckResolution_pinball_marker_far-distance.png

[ARToolKit_NFT_-_dispFeatureSet_terminal]: /ARToolKit_NFT_-_dispFeatureSet_terminal.png
[ARToolKit_NFT_-_dispFeatureSet]: /ARToolKit_NFT_-_dispFeatureSet.png

[ARToolKit_NFT_-_dispImageSet_terminal]: /ARToolKit_NFT_-_dispImageSet_terminal.png
[ARToolKit_NFT_-_dispImageSet]: /ARToolKit_NFT_-_dispImageSet.png