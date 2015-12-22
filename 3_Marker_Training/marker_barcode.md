# Using 2D-Barcode Markers
ARToolKit is well known for the appearance of its [markers][marker_about]: square markers with a black border, and with an arbitrary user-definable image in the interior. The "Hiro" marker used by default in the ARToolKit examples is an iconic example.

Multiple markers can be used to represent different objects or coordinate systems in an AR application. Additionally, a pattern can perform an important function in calculating the orientation of a square marker, since a pattern, being rotationally asymmetric, distinguishes between the four possible orientations of a marker in two dimensional space (the marker plane).

However, using arbitrary patterns inside a marker comes at some computational cost. The interior of every black square in the image captured from the camera must be compared against every known marker pattern at all four possible orientations. For a handful of markers, this computation comes at small cost, but as the number of markers in use in a single tracker rises to 20 or 100; the cost becomes significant. Additionally, pattern based markers are more likely to be confused by the tracker when there are a large number of markers (since there is a lower degree of uniqueness within the set of markers), leading to markers being misrepresented as each other.

The solution to the tracking difficulties caused by large number of markers is to use so-called two-dimensional barcode (2D-barcode) markers. These markers no longer have arbitrary user-defined patterns in the interior. Instead, they have a predetermined pattern of black and white squares in a simple grid arrangement (matrix pattern). ARToolKit treats the squares in a matrix pattern as a 2D-barcode; each unique matrix pattern being associated with an predetermined identifier.

2D-barcode markers are recognized in constant time meaning that different 2D-barcodes will take about the same amount of computer time to be recognized. Therefore, a large numbers of 2D-barcodes can be used in a scene at little additional computational cost. Additionally, when using 2D-barcode markers, there is a lower probability of one marker being mistaken for another. The downside is of course that the pattern inside the printed markers is no longer pictorial.

##Changing the Barcode Dimensions
A  2D-barcode marker with a 3x3 matrix of squares yields 64 rotationally unique patterns that are associated with predetermined identifiers (IDs). If more than 64 patterns are required, the dimensions of the barcode template can be increased. At present, this setting is not adjustable at runtime, so in order to make the change you must edit a configuration file and [recompile ARToolKit][build_artoolkit]. To generate 2D-barcodes larger than 3x3, the ARToolKit 2D-barcode dimension, and keep the ARToolkit default, make a separate copy of ARToolKit before making the dimension change.

The barcode dimension is set by the values `AR_PATT_SIZE2` and `AR_PATT_SAMPLE_NUM2` in the file `include/AR/arConfig.h`. Set the first value to the number of squares in each dimension, and the second to an integer multiple of the first. The default values are 3 and 9, respectively.

In general, it is better to use the smallest pattern size possible, as this helps the patterns to be recognized more easily at a greater distance. This table shows the number of barcodes possible with each pattern size:

| AR_PATT_SIZE2 | Number of barcodes possible |
|---------------|-----------------------------|
| 3             | 64                          |
| 4             | 8 192                       |
| 5             | 4 194 304                   |
| 6             | 8 589 934 592               |
| n             | `2^(n*n - 3)`               |

##2D-Barcode Markers as Multi-Markers
Multi-markers, not to be confused with the concept of multiple markers discussed above, are marker types that are made up of many sub-markers that are recognized and tracked as a single marker entity. This is opposed to recognizing and tracking multiple markers separately in a camera view. Patterns made up of a grid (matrix) of 2D-barcode markers are the default configuration for multi-marker sets, since they offer such radical performance improvements over other marker types with the use of multi-markers. Another advantage of multi-markers over traditional markers is that a multi-marker can still be recognized and tracked when some sub-markers are occluded from camera view.

The default barcode dimension for 2D-barcode markers in ARToolKit is a 3x3 pattern. For 3x3 2D-barcodes, there are 64 rotationally unique pattern arrangements making the marker suitable for augmented reality - enough patterns for most tabletop AR applications. You will find “.png” graphic files representing the 64 2D-barcode patterns in the ARToolKit SDK download; see folder path “[downloaded ARToolKit SDK]/doc/patterns/Matrix code 3x3 (72dpi)/”. These files can be printed.

The easiest way to use multi-markers in ARToolKit is to make a multi-marker dataset that consists of barcode markers. In order to do this, you only need to specify the number of markers, the ID of the barcodes involved, and their relative position to one another. For example, a single multi-marker dataset can be configured to track six unique sub-markers each affixed to six sides of a cube, allowing you to track a cube as a single object. This is done by defining a single multi-marker dataset that is configured with six sub-markers, the ID of the sub-markers (e.g. IDs 0–5), and where the sub-markers are relative to one another (rotationally and distance-wise). Due to the unique advantage multi-markers have for track-ability, the cube is still recognized and tracked despite the impossibility that all sides of a cube can be simultaneously in camera view.

For more information on multi-markers, including their configuration, visit the [multi-marker page][marker_multi].

[marker_about]: 3_Marker_Training:marker_about
[marker_multi]: 3_Marker_Training:marker_multi
[build_artoolkit]: 8_Advanced_Topics:build_artoolkit
