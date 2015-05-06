# ARToolkit NFT Utilities: checkResolution

## Purpose

The checkResolution tool supplied with ARToolKit NFT can help in determining the required resolution of source image data used in creating an NFT dataset.

## Operational summary

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

## Using the output

Moving the camera around and observing the DPI values should give you an idea of the maximum resolution required when producing the digital version of the printed material to be tracked (although as mentioned [here][1], it is not recommended to produce imagery at a higher resolution than the printed version, which is typically 150dpi). Additionally, the output helps determine the range of resolutions required when running the genImageSet tool as the first step in training a new NFT data set.

## Solving problems

Be sure to use a camera running at the same frame size as will be used in the online tracking process; the DPI values produced depend on the camera image size. In spite of megapixel webcams being the norm, it is actually better to use a lower resolution camera with a higher frame rate; 640x480 is perfectly adequate for most NFT tracking situations.

## Keyboard / mouse controls

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

[1]: /Training_ARToolKit_NFT_to_a_new_surface#Decide_on_the_image_set_resolutions

[Pinball_NFT_sample_printed_with_hand]: /Pinball_NFT_sample_printed_with_hand.JPG
[Hiro_marker_on_paddle_40mm]: /Hiro_marker_on_paddle_40mm.jpg 
[CheckResolution_pinball_marker_mid-distance]: /CheckResolution_pinball_marker_mid-distance.png
[CheckResolution_pinball_marker_close-distance]: /CheckResolution_pinball_marker_close-distance.png
[CheckResolution_pinball_marker_far-distance]: /CheckResolution_pinball_marker_far-distance.png