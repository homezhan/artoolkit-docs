#Natural Feature Tracking with Fiducial Markers
A fiducial marker is an *easily* detected feature in proximity to and as a point of reference to an object targeted for tracking. Fiducial markers can be knowingly and intentionally placed or naturally exist in a scene. Natural Feature Tracking (NFT) is the idea of recognizing and tracking a natural scene that is not (seemingly) augmented with markers. NFT can use embedded fiducial markers in a natural pictorial view to enhance tracking points and regions within the view. The result can be seemingly marker-less tracking (since the fiducial markers need not be obvious to the human viewer). Although ARToolKit offers full marker-less tracking, there are situations where using one or more [fiducial markers][marker_about] has advantages:

-   Using the NFT 1.0 tracker plus fiducial markers is less computationally expensive than NFT 1.0 + 2.0 full marker-less tracking. Thus NFT 1.0 with fiducial markers is more practical for mobile devices.
-   The NFT 2.0 tracker has a practical limit on the number of distinct markers that can be distinguished at any one time. Thus, if a large number of images need to be tracked (e.g. a 100-page book), fiducial markers enable efficient identification of numerous images intended to be tracked.
-   Fiducial marker tracking adds significant robustness to tracking, particularly in poor lighting conditions, or when the camera is far away from the tracked image.

##Fiducial Marker Appearance and Placement
To use only the standard 1.0 version of ARToolKit's NFT tracking with a fiducial marker, the tracked surface must have the marker either in the image or around the outside of it, there must be at least one in each image, the marker(s) must be square, and the markers must all have a black border and lie on a white background, or vice-versa. The marker(s) are not required to be of a particular size and the marker can embed colored patterns that blend with the image background.

Once the image is in digital form, you should add the fiducial marker to it. The marker(s) can have black or white borders. If using black borders, the marker must sit on an area of white or very light-colored background (add an extra white border around the black border if necessary). If using white borders, the marker must sit on an area of black or very dark colored background. The inner half of the marker forms the unique portion, i.e. for a marker 80 mm wide, the inner 40 mm in both vertical and horizontal dimensions is the unique portion.

![MagicLand3 embedded fiducial][magicland3_embedded_fiducial]

The marker does not have to be inside the portion of the image which is used as the NFT surface. It can be outside it, as these two examples demonstrate:

![In this NFT surface, fiducial markers have been placed around the textured portion, in a "filmstrip" arrangement".][example_2]
![In this NFT surface, 2 large and 4 small fiducial markers have been placed at right of the textured portion.][example_3]

We can revisit the bottle-label image from the [Training NFT to a new surface][1] tutorial with the aim of embedding a marker into the label image. If we choose the pattern (the inner-part of the marker) so that it contains some of the background, then the marker will be even less intrusive.

![The bottle and label design to be tracked, modified to create some space to place the marker.][butterworth_modified_for_marker]
![The marker design. The marker border is white, so it must sit on a dark background.][butterworth_marker]
![The label with the fiducial marker embedded. A black background has been added around the marker.][butterworth_with_marker]
![The new rectangular area to be used for NFT data][butterworth_modified_highlighted]
![Close-up of the new area to be used for NFT data. Note that in this case, part of the fiducial marker also forms part of the NFT dataset.][butterworth_modified_tracked]

## Training the System to the Embedded Fiducial Marker(s)
If implementing an app using standard ARToolKit NFT in which one or more fiducial markers is required, an image and markers input set configuration file (.iset) is required to generate recognition and tracking data set files. The generated files are a marker file (.mrk) and one (or more) pattern files (.pat-xx).

From the command-line, execute the ARToolKit utility genMarkerSet.exe with the input set configuration file (.iset) as an argument:

| Windows Desktop (Android/WinRT devices) | Mac OS X (Android/iOS devices) | Linux (Android devices) |
| :------------ | :------- | :------------ |
| genMarkerSet.exe mycoolimage.iset | ./genMarkerSet mycoolimage.iset | ./genMarkerSet mycoolimage.iset |

You will see two numbers; the first, the number of candidate markers in the image, and the second, the number of markers that pass a goodness test (making sure that the marker is square and with clean edges) and which are candidates for training. If the second number is 0, then no candidate markers were found; a result that will send you right back to the very start of the process - creating an image with an embedded marker(s)!

If the markers are detected then their positions will be displayed in a window, and you will be prompted to accept or reject each one. Type 'y' and press return to accept the marker. After this step, the utility prompts for a filename to save the dataset.

Once the training has completed, you should move the *.mrk* file and the *.pat-xx* files into the same folder as the *.iset* file from which they were generated. That way, the software will automatically locate them.

## Testing with The "nftSimple" App Example
The easiest means of testing NFT datasets you have trained is to run them using the **nftSimple** example program (ARToolKit NFT versions to 5.X) or "exampleNFTWithFiducial" example program (ARToolKit v5.X). Open a console window and change to the ARToolKitNFT bin directory.

Run nftSimple.exe from the command-line providing a relative path to the config.dat file as a command-line argument. The previous *MagicLand3* sample dataset example has been deprecated. A newer nftSimple demonstration is to be provided (TBP).  E.g, to launch nftSimple with the [newer example TBP] sample dataset:

| Windows Desktop (Android/WinRT devices) | Mac OS X (Android/iOS devices) | Linux (Android devices) |
| :- | :- | :- |
| nftSimple.exe Data\[newer example TBP]\config.dat | ./nftSimple.app/Contents/MacOS/nftSimple Data/[newer example TBP]/config.dat | ./nftSimple Data/[newer example TBP]/config.dat |

The tracking in this application is initialized by the appearance of a marker. Once a marker is detected, tracking is switched to feature based and the marker is no longer necessary. Red 3D boxes are drawn on the images. If feature tracking failed, it is changed back to marker based tracking and yellow 3D boxes are drawn.

For more information continue to the page [Running the nftSimple example][2]

A more complex example, showing the use of 2D-barcode markers outside the NFT surface can be downloaded [here][3].

[marker_about]: 3_Marker_Training:marker_about
[1]: 3_Marker_Training:marker_nft_training
[2]: 7_Examples:example_nftsimple
[3]: http://www.artoolworks.com/support/attachments/ARToolKikt%20NFTv1%20sample%20dataset%20(map%20of%20Christchurch%2C%20NZ).zip

[magicland3_embedded_fiducial]: :magicland3_embedded_fiducial.png
[example_2]: :nft_example_2.jpg
[example_3]: :nft_example_3.jpg
[butterworth_modified_for_marker]: :nft_example_mrs_butterworths_modified_for_marker.jpg
[butterworth_marker]: :nft_example_mrs_butterworths_marker.jpg
[butterworth_with_marker]: :nft_example_mrs_butterworths_with_marker.jpg
[butterworth_modified_highlighted]: :nft_example_mrs_butterworths_modified_for_marker_area_highlighted.jpg
[butterworth_modified_tracked]: :nft_example_mrs_butterworths_modified_for_marker_tracked_area.jpg
