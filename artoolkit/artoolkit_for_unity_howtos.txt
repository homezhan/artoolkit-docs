[Main Page](/Main_Page "wikilink") \> [ARToolKit for
Unity](/ARToolKit_for_Unity "wikilink") \>

Control The View Layout
-----------------------

The developer can choose how the input video's aspect ratio is treated
in respect to the display's aspect ratio. If they do not match, such as
4:3 video on a 16:10 screen, then the developer can choose either to
stretch the video (which will introduce distortion), or use less of the
screen (which will introduce empty bars). Any bars will have the color
of the background clearing camera which always renders to the entire
screen.

-   **Fill screen**: Possibly stretch the rendering and introduce
    distortion.
-   **Maintain video aspect ratio (bars)**: Correct rendering, but bars
    at edges if the video is more square than display, or at top and
    bottom if display is more square than video.
-   **Maintain video aspect ratio (overfill screen)**: Unfortunately
    this mode is unavailable because Unity does not permit viewport
    rectangles outside the bounds of the screen.

Calibrate the camera
--------------------

ARToolKit's calib_camera utility is included with ARToolKit for Unity
in the bin/ directory. See [Calibrating your
camera](/Calibrating_your_camera "wikilink") for usage instructions.

Generate new marker files
-------------------------

### Square marker patterns

The mk_patt command-line utility is the supported means of generating
new pattern files for ARToolKit markers. The ARToolKit for Unity Windows
installer / Mac OS X .zip file include mk_patt in the bin/ directory.
See [Creating and training new ARToolKit
markers](/Creating_and_training_new_ARToolKit_markers "wikilink") for
usage instructions.

### NFT datasets

See
[ARToolKit_for_Unity_Using_NFT\#Generating_new_NFT_datasets](/ARToolKit_for_Unity_Using_NFT#Generating_new_NFT_datasets "wikilink")

Use optical see-through
-----------------------

See
[Using_an_optical_see-through_display\#ARToolKit_for_Unity](/Using_an_optical_see-through_display#ARToolKit_for_Unity "wikilink")
and
[Using_an_optical_see-through_display\#ARToolKit_for_Unity_2](/Using_an_optical_see-through_display#ARToolKit_for_Unity_2 "wikilink")

[Category:ARToolKit for Unity](/Category:ARToolKit_for_Unity "wikilink")