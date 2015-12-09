#About the Traditional Template Square Marker
ARToolKit applications allow virtual imagery to be superimposed on the live environment through a video or see-through display. Although this appears magical, the secret is in the black square, referred to as a **square marker**. A square marker is made up of a light colored, surrounding, **padding**, usually white, surrounded by a thick dark colored, usually black, **border** and an embedded, high contrast, image content, referred to as a **pattern**. The pattern is what makes a square marker unique. Square markers are recognized, tracked and is used to calculate position in 3D space. The ARToolKit augmented reality works as follows:

1.  The camera captures video of the camera view and sends it to the computer.
2.  Software on the computer searches through each video frame for any square shapes (square markers).
3.  If a square marker is found and the image content embedded by the square, the pattern, is matched and identified, the software uses mathematics to calculate, relative to the camera, both the position of the black square and the pattern orientation .
4.  Once the position and orientation of the camera are known, a computer graphics model is drawn using an offset to the calculated position and with a matching orientation.
5.  This model is drawn in the foreground of the captured video and tracked against the movements of the background video causing the model to appear attached to the background.
6.  The final output is shown back in the display, so when the user looks through the viewer, they see the rendered graphic model over a real world video stream; seemingly homogeneous with the camera view.

The figure below summarizes these steps. ARToolKit is able to perform this camera tracking in real time, ensuring that the virtual objects always appear overlaid on the tracking markers.

![The ARToolKit tracking process][diagram]

####Some Terminology
The traditional template marker can be applied to several marker types of varying names that can lead to some terminology confusion. Some of these markers types that share many similar characteristics are known separately as square markers, 2D-barcodes and matrix markers. This page is about square markers.

##Limitations
While vision-based tracking is exciting in enabling so many applications, there are limitations which affect ARToolKit and other vision based systems.

###Occlusion
Naturally the virtual objects will only appear when the marker being tracked is in camera view. This may limit the size or movement of the virtual objects. It also means that if users cover up, from the camera's view, part of the marker with an obstruction, the composited virtual model disappears. Also, if the marker borders are moved outside the camera's view, the marker will be clipped, no longer having four corners. As a result, recognition will fail. 

###Range
There are also range issues in optical tracking, since as markers are move further away from the camera, the markers occupy fewer pixels in the camera's view and results in having insufficient detail for recognition, tracking and identification. The larger the physical embedded marker pattern, the further away the embedded marker pattern can be detected and so the greater the track-ability of the marker.

Table 1 shows some typical maximum ranges for square markers of different sizes. These results were gathered by scanning square markers of increasing size, placing them perpendicular to the camera and increasing the distance between the camera and marker until the marker is no longer recognized.

| Pattern Size (inches)  |  Usable Range (inches) |
| :---------------------------: | :-------------------------------:
| 2.75                              | 16
| 3.50                              | 25
| 4.25                              | 34
| 7.37                              | 50
[Table 1: Tracking range of different size square markers]

In order to increase the usable range, choosing marker images with lower complexity will help. Marker images with large black and white regions (i.e. low frequency patterns) are the most effective. Replacing the marker's pattern of the 4.25 inch square marker (used above) with a pattern of significantly increased complexity reduced the tracking range from 34 to 15 inches.

Think of low optical frequency images as images made up with pixel values that change little and infrequently over the two dimension space the image occupies. And, inversely, high frequency images are made up of pixel values that change greatly and often.  Recognition and tracking are best served by patterns made up of a simple, rotationally asymmetrical, low frequency, image. Or a low number aggregation of contrasting low frequency images. That is, marker patterns of simple shapes of no and little detail.

An alternative to using traditional template square markers is [2D-barcode markers][marker_barcode]. These markers have a matrix of black and white squares in the interior of the marker producing a unique pattern. 2D-barcodes can have a much lower optical frequency than traditional template square markers depending on the complexity of the pattern content. You are also able to [make your own square markers][marker_training].

### Marker's Planar Orientation to the Camera
Tracking is also affected when the orientation of the two dimensional  plane that the marker lies on is not perpendicular to camera's view. That is, some camera-view-to-marker orientation *other than* a marker laying flat on a table top and a camera hovering straight up above while the camera's lens is pointed straight down at the marker. As the camera's view become more tilted horizontally relative to the marker's plane (to the table top), less and less detail of the marker is visible and and it becomes un-recognitionable.

### Lighting Conditions
Finally, the tracking results are also affected by lighting conditions. Overhead lights may create reflections and glare spots on a paper marker and so make it more difficult to find the marker square. Shadows can be cast across the paper, breaking up white areas in the camera image.

To reduce the glare, markers should be constructed of or over non-reflective surfaces. For example, by gluing black velvet fabric to a white base. The 'fuzzy' velvet paper available at craft shops also works very well.

To reduce shadows, we recommend using omnidirectional lighting (lighting conditions where light falls on the markers from all directions).

[diagram]: :diagram.jpg
[marker_barcode]: 3_Marker_Training:marker_barcode
[marker_training]: 3_Marker_Training:marker_training
