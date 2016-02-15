# Training ARToolKit Natural Feature Tracking (NFT) to Recognize and Track an Image
ARToolKit NFT is able to recognize and track natural features of photos and documents, specifically, **planar textured surfaces**. However, to accomplish this, ARToolKit NFT requires that the visual appearance of the surface is known in advance. Thus,  the system has to be *trained* with a surface in advance to recognize and track the surface. The output of this training is a set of data that can be used for realtime tracking in application using the ARToolKit SDK.

The following constraints apply to surfaces which can be used with ARToolKit NFT.

-   The surfaces to be tracked must be supplied as a rectangular image.
-   The images must be supplied in jpeg format.
-   The surface must be textured and have a reasonable amount of fine detail and sharp edges (a low degree of [self-similarity][self-similarity] and high spatial-frequency). Images with large areas of single flat color, that are blurred or have soft detail will not track well, if at all. In such images, it's difficult to locate distinct feature points.
-   Larger or higher resolution images (more pixels) will allow the extraction of feature points at higher levels of detail, and thus will track better when the camera is closer to the image, or when a higher resolution camera is used.

The ARToolKit NFT tracker, does not require augmenting the image with [fiducial markers][marker_nft_fiducial_markers]  to implement NFT tracking. But, for increased efficiency and robustness, fiducial markers can be used along with NFT markers as part of the dataset when using the NFT tracker.

##Typical Workflow Summary for Training an Image to be NFT Recognized and Tracked

1.  If the image to be recognized and tracked is hardcopy, the image must be scanned or camera captured into a jpeg formatted soft-copy image file. A high-resolution, high-quality soft-copy image forms the basis for locating feature points and generating the *trained* dataset. 
2.  The resulting soft-copy image is used as input to the NFT training applications.
3.  Produce and prepare the final hardcopy image that is recognized and tracked.

A good example of an NFT image is "[pinball.jpg][3]" (found under the path: [downloaded ARToolKit SDK root directory]/doc/Marker images).

###Producing a High-Resolution, High-Quality Soft-Copy Image for NFT Training
The NFT tracker works by looking for a known feature points defined by a dataset, which is a representative descriptor of the image you want to track. This section will guide you to producing a high-quality soft-copy image for NFT tracking.

Care must be taken to ensure that the image supplied to the training tools is not too big (wasteful of memory, disk and CPU during tracking) and not too small (of insufficient detail to allow tracking when the camera is close to the image). Whether starting from a pre-existing print, or a soft-copy image, the considerations for resolution and target size are the same:

1.  What is the physical size of the printed material? I.e., what is the width and height in inches or millimeters? Measure this accurately with a ruler. Common paper sizes include A4 (210mmX297mm) and US Letter (8.5 inchesX11inches, or 215.9mmX279.4mm). ![Measuring the size with a millimeter rule. Measure the part that corresponds exactly to your source image. Don't include the border.][NFT_example_KPM_measuring_image_with_rule]
2.  When NFT tracking, how close to the camera will the printed image be when in use? This relates to the required *resolution*, commonly expressed as pixels or dots per inch (DPI). Most laser printers produce 300 dpi black and white images, while color printers usually use a dot-screen at 150 dpi (although they may advertise higher resolutions, almost all use a 150 dpi resolution). To help answer the resolution question, use the "[checkResolution][marker_nft_utilities]" tool supplied with ARToolKit (found under the path: [downloaded ARToolKit SDK root directory]/bin). Once you have determined the maximum resolution required, return to this page.

For example, borderless A4 at 150 dpi is 1240 pixels wide and 1754 pixels tall. Borderless US Letter at 150 dpi is 1275 pixels wide and 1650 pixels tall. If producing from digital artwork at 1:1 scale, you can use image size from that artwork. ![Example here is from Adobe Photoshop.][NFT_example_KPM_image_size_photoshop]

If the measurements are in millimeters, you can convert to inches by dividing by 25.4 millimeters per inch:
<pre>
    inches = millimeters / 25.4 millimeters per inch
</pre>

####Using a Hardcopy Image Source
In many cases, it may be simplest to start with a hardcopy image of the surface to be tracked. Further considerations for starting with a hardcopy image:

-   Augmenting the pages of a book, magazine, or other printed material for which you do not have the source design artwork.
-   Digital artwork's prints differs considerably in brightness, color or tone than its soft-copy counterpart.

If using a scanner or camera that needs a "resolution" setting, you can just directly use the maximum resolution calculated by the *checkResolution* tool (found under the path: [downloaded ARToolKit SDK root directory]/bin).

If using a scanner or camera that expresses resolution in terms of *dots per inch*, calculate the required pixel resolution. The calculation:

    width in pixels = width in inches * dots per inch
    height in pixels = height in inches * dots per inch

If using a scanner or camera that requires a "megapixels" setting, calculate the required width and height in pixels (above) , then multiply these together and divide the result by 1,000,000. Example:

    640 width in pixels * 480 height in pixels = 307,200 pixels of resolution
    307,200 pixels / 1,000,000 pixels/megapixel = ~0.31 megapixels of resolution

After scanning or photography is completed, check that the resulting digital image is not blurred and has sufficient contrast. Washed-out blurry images work very poorly in the NFT training process.

#####Using a Hardcopy Image Sourced from Digital Artwork Soft-Copy
Using soft-copy digital artwork as input to the training process versus using the printed hardcopy of the digital art can result in significant differences in trained features that will reduce the robustness of the tracking of the final hardcopy surface. Also, if the scale of the artwork soft-copy used in the training process differs from the scale of the final hardcopy surface used for tracking, misleading tracking can result. Therefore, it's recommended to start the training process by printing the digital artwork soft-copy and use the resulting printed hardcopy as the eventual input soft-copy image for the training process.

Producing the digital image for tracking from pre-existing digital artwork is simple. First print the digital artwork referring to the two previous sections.
After printing your digital artwork, check that the print is the correct size. Also, check that the print matches the artwork in terms of contrast, absence of print defects, etc.

###Generating an NFT Dataset from the Digital Image - the Training Steps
Now that you have an image you wish to use with NFT, you must create the dataset (train the image). Surface training uses [utilities][marker_nft_utilities] included in the ARToolKit package. These utilities must be run from the command line. On Linux / OS X open a terminal window and cd to the bin directory. On Windows, this means you must open a “cmd” console and cd to the bin directory.

####Training Step 1: Decide on the Image Set Resolutions
Most of the operation of the training utility programs proceeds without much input from the user, but there is one important decision required prior to starting the training utility; that is selecting the resolutions at which features of the image will be extracted. (Generally, features are extracted at three or more resolutions to cope with the fact that dots in the image will appear at different resolution to the software depending on how close or far away the camera is from the image.)

For a typical webcam operating at VGA (640x480) resolution and tracking at handheld-distance from the surface, a range of resolutions between 20 dpi and 120 dpi is a good starting point. If using a higher-resolution webcam or tracking much closer to the surface, higher resolutions will be required. *Note: that there is no point in using resolutions higher than the actual resolution of the final printed surface!*

The utility application "[checkResolution][marker_nft_utilities]" (found under the path: [downloaded ARToolKit SDK root directory]/bin) can help with the decision of what values to use as minimum and maximum resolutions.

After completing a training pass, it will pay to come back to the choice of image set resolutions and experiment with different minimum and maximum resolutions. The choice depends greatly on the way in which you intend to use ARToolKit for tracking, and your source images.

If you have further questions, you should ask questions to the ARToolKit community on the [forum][forum].

####Training Step 2: Generating an NFT Dataset from the Digital Image

The same NFT dataset generation tools are shared between all supported ARToolKit desktop and mobile platforms. Dataset generation is performed using a single integrated tool ""[genTexData][marker_nft_utilities]"".

After setting any required video configuration, launch the genTexData tool:

![Launch the program from a terminal window, supplying the name of the input JPEG file as the parameter.][NFT_example_genTexData_010]

![You can specify how selective the training algorithms should be in rejecting candidate tracking features.][NFT_example_genTexData_020]

In the first step, the source image is resampled at multiple resolutions, generating an image set (.iset) file. This contains raw image data that will be loaded into the app at runtime for tracking.

You may be prompted for the source image resolution, as well as the range of resolutions you wish to use for tracking. (See the preceding section for advice on how to choose a good set of resolutions to use.) Enter the minimum and maximum resolutions at the terminal prompt. You can enter decimal values (numbers with a '.'). These values can also be manually specified on the command line. (See the list of command line options below.)

![The utility will load the JPEG and read its size and expected printed resolution. If no resolution value is embedded, you will be prompted to supply the resolution.][NFT_example_genTexData_030]

![Specify the minimum and maximum resolution values for tracking. A suitable image set will then be automatically generated from this range, and saved to disk with the suffix".iset".][NFT_example_genTexData_040]

![The utility begins to generate tracking data. This procedure may take some time, even on a fast CPU.][NFT_example_genTexData_050]

![When generation of tracking data is complete, the utility will save the ".fset" and ".fset2" files to disk alongside the .jpeg. Training is then complete.][NFT_example_genTexData_060]

####Training Step 3: Testing the Dataset
Once the image set and feature sets have been generated, you can use the [dispImageSet and dispFeatureSet][marker_nft_utilities] utilities to examine the output of the training process.

By examining the output of dispFeatureSet, you can immediately see a number of things about the image used:

-   Flat areas with no texture provide no features to track. You should use source material with plenty of edges and fine surface detail.
-   Blurry areas (such as the blurry face at the bottom of the printed image) are also poor areas for tracking.
-   Some areas with fine detail but low contrast will be quite "noisy", with a slight adjustment of the image size or other training parameters resulting in these features not being chosen.

The easiest means of testing NFT datasets you have trained in live tracking is to run them using the [nftSimple example][example_nftsimple] program.

###Producing and Preparing the Final Hardcopy Image that is Recognized and Tracked
Whether working from supplied printed material or a print from digital artwork, eventually the user needs an actual surface to hold in front of the camera to recognize and track the trained image.

 The soft-copy image is printed using a high-quality color printer, on low-gloss paper. It is important that the image surface is kept as flat as possible. Small amounts of curvature can be coped with by the tracker to some degree, but flat is best. Where possible, the print should be on or affixed to a physical prop that keeps it flat.

![Glue printed pages to a flat surface using a dry glue. Take care not to distort the printed paper when affixing.][Glueing_marker_to_backing_board]

For Example: If you were printing a label to be attached to a product, the label should be applied to a flat area of the product. The curved surface of a bottle or can would not be suitable, and alternatives could include the packaging holding the bottle or can, or on a flat label or tag attached to the product. If mounting in a book, surfaces should be printed on heavy card and bound with board-book, ring or spiral binding. If used as an unbound card, affix to the card with a dry glue (e.g. a glue stick or an industrial dry adhesive).

[self-similarity]: https://en.wikipedia.org/wiki/Self-similarity
[marker_nft_fiducial_markers]: 3_Marker_Training:marker_nft_fiducial_markers
[marker_nft_utilities]: 3_Marker_Training:marker_nft_utilities
[example_nftsimple]: 7_Examples:example_nftsimple
[forum]: http://www.artoolworks.com/support/forum/

[3]: :pinball.jpg

[NFT_example_KPM_measuring_image_with_rule]: :nft_example_kpm_measuring_image_with_rule.jpg
[NFT_example_KPM_image_size_photoshop]: :nft_example_kpm_image_size_photoshop.jpg
[Glueing_marker_to_backing_board]: :glueing_marker_to_backing_board.jpg
[NFT_example_genTexData_010]: :nft_example_gentexdata_010.png
[NFT_example_genTexData_020]: :nft_example_gentexdata_020.png
[NFT_example_genTexData_030]: :nft_example_gentexdata_030.png
[NFT_example_genTexData_040]: :nft_example_gentexdata_040.png
[NFT_example_genTexData_050]: :nft_example_gentexdata_050.png
[NFT_example_genTexData_060]: :nft_example_gentexdata_060.png
