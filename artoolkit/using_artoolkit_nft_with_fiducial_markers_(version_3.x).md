# Using ARToolkit NFT with Fiducial Markers

## Why use ARToolKit NFT with fiducial markers?

Although ARToolKit NFT 2.0 offers full markerless tracking, there are some situations where using one or more markers as part of an image is worthwhile:

-   Using the NFT 1.0 tracker plus fiducial markers is less computationally expensive than NFT 1.0 + 2.0 markerless tracking. It thus works better on mobile devices.
-   The NFT 2.0 tracker has a practical limit on the number of distinct markers which can be distinguished at any one time. Thus if a large number of images need to be tracked (e.g. a 100-page book) fiducial markers can help identify which image needs to be tracked.
-   Fiducial marker tracking adds significant robustness to tracking, particularly in poor lighting conditions, or when the camera is far away from the tracked image.

## Fiducial marker appearance and placement

To use only the standard 1.0 version of ARToolKit NFT with a fiducial marker, the tracked surface must have the marker either in the image, or around the outside of it,. There must be at least one in each image (optionally more than one). The marker(s) must be square, and must all have a black border lying and lie on a white background, or vice-versa. The marker(s) do not have to be any particular size, and the contents of the marker can be in colour.

Once the image is in digital form, you should add the fiducial marker to it. The marker(s) can have black or white borders. If using black borders, the marker must sit on an area of white or very light-coloured background. (Add an extra white border around the black border if necessary.) If using white borders, the marker must sit on an area of black or very dark coloured background. The inner half of the marker forms the unique portion, i.e. for a marker 80 mm wide, the inner 40 mm in both vertical and horizontal dimensions is the unique portion.

A black-bordered marker must sit on a white or near-white background. Where the background is not white, as in the example MagicLand3 image below, an extra area of white background must be added around the marker

[Image:MagicLand3 embedded fiducial.png](/Image:MagicLand3_embedded_fiducial.png "wikilink")

The marker does not have to be inside the portion of the image which is used as the NFT surface. It can be outside it, as these two examples demonstrate:

<File:NFT> example 2.JPG|In this NFT surface, fiducial markers have been placed around the textured portion, in a "filmstrip" arrangement".]]
<File:NFT> example 3.JPG|In this NFT surface, 2 large and 4 small fiducial markers have been placed at right of the textured portion.]]

We can revisit the bottle-label image from the [Training ARToolKit NFT to a new surface](/Training_ARToolKit_NFT_to_a_new_surface "wikilink") tutorial with the aim of embedding a marker into the label image. If we choose the pattern (the inner-part of the marker) so that it contains some of the background, then the marker will be even less intrusive.

<File:NFT> example Mrs Butterworths modified for marker.jpg|The bottle and label design to be tracked, modified to create some space to place the marker.
<File:NFT> example Mrs Butterworths marker.jpg|The marker design. The marker border is white, so it must sit on a dark background.
<File:NFT> example Mrs Butterworths with marker.jpg|The label with the fiducial marker embedded. A black background has been added around the marker.
<File:NFT> example Mrs Butterworths modified for marker area highlighted.jpg|The new rectangular area to be used for NFT data
<File:NFT> example Mrs Butterworths modified for marker tracked area.jpg|Close-up of the new area to be used for NFT data. Note that in this case, part of the fiducial marker also forms part of the NFT dataset.

## Training the system to the embedded fiducial marker(s)

If using the standard ARToolKit NFT, in which one or more fiducial markers is required, in this step the fiducial marker(s) you embedded in the image are recognised and trained. The output of this step is a marker file (.mrk) and one (or more) pattern files (.pat-xx).

Run genMarkerSet.exe providing the imageset as command line argument. E.g.: Windows: genMarkerSet.exe mycoolimage.iset Linux / Mac OS X: ./genMarkerSet mycoolimage.iset

You will see two numbers, the first the number of candidate markers in the image, and the second the number of markers which pass a goodness test (making sure that the marker is square and with clean edges) and which are candidates for training. If the second number is 0, then no candidate markers were found – a result which will send you right back to the very start of the process .. creating an image with an embedded marker.

If you have got detected markers (thankfully usually the case!) then their detected positions will be displayed in a window, and you will be prompted to accept or reject each one. Type y and press return to accept a marker, and then enter a filename to save it under.

Once the training has completed, you should move the .mrk file and and the .pat-xx files into the same folder as the .iset file from which they were generated. That way, the software will automatically locate them.

## Testing with the simpleNFT example

The easiest means of testing NFT datasets you have trained is to run them using the **simpleNFT** example program (ARToolKit NFT versions to 3.49.0) or '"exampleNFTWithFiducial" example program (ARToolKit v3.50.0). Open a console window and change to the ARToolKitNFT bin directory.

Run simpleNFT.exe providing the relative path to the config.dat file as command line argument. E.g, to launch simpleNFT with the MagicLand3 sample dataset.:

-   Windows: simpleNFT.exe Data/MagicLand3/config.dat
-   Mac OS X: ./simpleNFT.app/Contents/MacOS/simpleNFT Data/MagicLand3/config.dat
-   Linux: ./simpleNFT Data/MagicLand3/config.dat

The tracking in this application is initialized by the appearance of a marker. Once a marker is detected, tracking is switched to feature based and marker is no longer necessary. Red 3D boxes are drawn on the images. If feature tracking failed, it is changed back to marker based tracking and yellow 3D boxes are drawn.

For more information continue to the page [Running the simpleNFT example](/Running_the_simpleNFT_example "wikilink").

## Example NFT with fiducial marker dataset

A working example of an NFT dataset with an embedded fiducial marker is included with ARToolKit NFT, named "MagicLand3".

A more complex example, showing the use of 2D barcode markers outside the NFT surface can be downloaded here:
<http://www.artoolworks.com/support/attachments/ARToolKikt%20NFTv1%20sample%20dataset%20(map%20of%20Christchurch%2C%20NZ).zip>