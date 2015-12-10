# Training NFT to a New Surface
ARToolKit NFT tracks from natural features of planar textured surfaces (e.g. photos and documents). The current implementation of the tracking algorithm requires that the visual appearance of the surface is known in advance. Thus, in advance we have to *train* the system to the appearance of a particular surface that we want to use for tracking. The output of this training is a set of data that can be used for realtime tracking in our application.

The following constraints apply to surfaces which can be used with ARToolKit NFT.

-   The surfaces to be tracked must be supplied as a rectangular image.
-   The images must be supplied in jpeg format.
-   The surface must be textured and have a reasonable amount of fine detail (i.e. it must have a low degree of [self-similarity][self-similarity] and high spatial-frequency). Images with large areas of single flat color will not track well (if at all) since no unique features will be able to be identified in the interior of the areas of flat color, and images that are blurred or have soft detail will similarly not track well.
-   Larger or higher resolution images (more pixels) will allow the extraction of feature points at higher levels of detail, and thus will track better when the camera is closer to the image, or when a higher resolution camera is used.

The ARToolKit NFT 2.0 tracker does not impose any additional constraints. For increased efficiency and robustness, you are allowed to [use fiducial markers along with NFT markers as part of the dataset][marker_nft_fiducial_markers], which utilizes the NFT 1.0 tracker.

##Producing a Good NFT Image
The NFT tracker works by looking for a known dataset, which is a representative descriptor of the image you want to track. This section will guide you to producing a high-quality image for NFT.

Summary: A typical workflow for producing NFT markers proceeds thus:

1.  A high-resolution image which is to form the basis of the marker is obtained. If the source texture is on paper, it must be scanned. The image is saved in jpeg format.
2.  The resulting image is fed into the NFT training applications.
3.  If the image is to be printed, print on a good-quality color printer, on low-gloss paper, to produce the final image which will be tracked.

A good example of an NFT image is "[pinball.jpg][3]".

Whether starting from a pre-existing print, or a digital image, the considerations for resolution and target size are the same:

1.  What is the physical size of the printed material? I.e., what is the width and height in inches or millimeters? Measure this accurately with a ruler. Common paper sizes include A4 (210 mm x 297 mm) and US Letter (8.5 inches x 11 inches, or 215.9 mm x 279.4mm). ![Measuring the size with a millimeter rule. Measure the part that corresponds exactly to your source image. Don't include the border.][NFT_example_KPM_measuring_image_with_rule]
2.  How close to the camera will the printed image be when in use? This relates to the required *resolution*, commonly expressed as pixels or dots per inch (DPI).Most laser printers produce 300dpi black and white images, while color printers usually use a dot-screen at 150 dpi (although they may advertise higher resolutions, almost all use a 150dpi resolution). To help answer the resolution question, use the "[checkResolution][marker_nft_utilities]" tool supplied with ARToolKit. Once you have determined the maximum resolution required, return to this page.

For example, borderless A4 at 150dpi is 1240 pixels wide and 1754 pixels tall. Borderless US Letter at 150dpi is 1275 pixels wide and 1650 pixels tall. ![If producing from digital artwork at 1:1 scale, you can use image size from that artwork. Example here is from Adobe Photoshop.][NFT_example_KPM_image_size_photoshop]

If you have the measurements in millimeters, you can convert to inches by dividing by 25.4 (i.e. there are 25.4 millimeters in one inch).
<pre>
    inches = millimeters / 25.4
</pre>

###Using a Physical Print
In many cases, it may be simplest to start with a physical print of the tracked surface. This might be also be best if:

-   You are augmenting the pages of a book, magazine, or other printed material for which you do not have the design artwork.
-   You have digital artwork, but the physical print differs considerably in brightness, color or tone.

If using a scanner or camera that needs a "resolution" setting, you can directly use the maximum resolution calculated by the checkResolution tool.

If using a scanner or camera that calculates in terms of image width and height, multiply the resolution calculated by the physical width and height: `width in pixels = width in inches x dots per inch` and  `height in pixels = height in inches x dots per inch`

If using a scanner or camera that requires a "megapixels" setting, calculate the required width and height in pixels (above) and then multiply these together and divide by 1,000,000. E.g. 640x480 = 0.3 megapixels.

After scanning or photography is completed, check that the resulting digital image is not blurred and has sufficient contrast. Washed-out blurry images work very poorly in the NFT training process.

###Using Digital Artwork
Producing the digital image for tracking from pre-existing digital artwork is simple. Care must be taken, however, to ensure that the image supplied to the training tools is not too big (wasteful of memory, disk and CPU during tracking) and not too small (of insufficient detail to allow tracking when the camera is close to the image.).

After printing your digital artwork, check that the print is the correct size. A scaled print will still track, but will give scaled (and potentially misleading) tracking results (distance from camera etc.). Also, check that the print matches the artwork in terms of contrast, absence of print defects etc. Differences between the digital artwork and the physical print will reduce the robustness of the tracking, as some of the trained features may not be present on the print.

##Physical Print Properties
Whether working from supplied printed material or a print from digital artwork, eventually the user needs an actual surface to hold in front of the camera.

It is important that the physical print is kept as flat as possible. Small amounts of curvature can be coped with by the tracker to some degree, but flat is best. Where possible, the print should be on or affixed to a physical prop that keeps it flat.

![Glue printed pages to a flat surface using a dry glue. Take care not to distort the printed paper when affixing.][Glueing_marker_to_backing_board]

For Example: If you were printing a label to be attached to a product, the label should be applied to a flat area of the product. The curved surface of a bottle or can would not be suitable, and alternatives could include the packaging holding the bottle or can, or on a flat label or tag attached to the product. If mounting in a book, surfaces should be printed on heavy card and bound with board-book, ring or spiral binding. If used as an unbound card, affix to the card with a dry glue (e.g. a glue stick or an industrial dry adhesive).

##Decide on the Image Set Resolutions
Most of the operation of the training utility programs proceeds without much input from the user, but there is one important decision required prior to starting the training utility; that is selecting the resolutions at which features of the image will be extracted. (Generally, features are extracted at three or more resolutions to cope with the fact that dots in the image will appear at different resolution to the software depending on how close or far away the camera is from the image.)

For a typical webcam operating at VGA (640x480) resolution and tracking at handheld-distance from the surface, a range of resolutions between 20 dpi and 120 dpi is a good starting point. If using a higher-resolution webcam or tracking much closer to the surface, higher resolutions will be required. *Note: that there is no point in using resolutions higher than the actual resolution of the final printed surface!*

The utility program "[checkResolution][marker_nft_utilities]" can help with the decision of what values to use as minimum and maximum resolutions.

After completing a training pass, it will pay to come back to the choice of image set resolutions and experiment with different minimum and maximum resolutions. The choice depends greatly on the way in which you intend to use ARToolKit for tracking, and your source images.

If you have further questions, you should ask questions to the ARToolKit community on the [forum][forum].

##Generating an NFT dataset from the Digital Image
Now that you have an image you wish to use with NFT, you must create the dataset (train the image). Surface training uses [utilities][marker_nft_utilities] included in the ARToolKit package. These utilities must be run from the command line. On Linux / OS X open a terminal window and cd to the bin directory. On Windows, this means you must open a “cmd” console and cd to the bin directory.

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

###Testing the Dataset
Once the image set and feature sets have been generated, you can use the [dispImageSet and dispFeatureSet][marker_nft_utilities] utilities to examine the output of the training process.

By examining the output of dispFeatureSet, you can immediately see a number of things about the image used:

-   Flat areas with no texture provide no features to track. You should use source material with plenty of edges and fine surface detail.
-   Blurry areas (such as the blurry face at the bottom of the printed image) are also poor areas for tracking.
-   Some areas with fine detail but low contrast will be quite "noisy", with a slight adjustment of the image size or other training parameters resulting in these features not being chosen.

The easiest means of testing NFT datasets you have trained in live tracking is to run them using the [nftSimple example][example_nftsimple] program.

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
