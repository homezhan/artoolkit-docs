# Using 2D-Barcode Markers
ARToolKit is well known for the appearance of its [markers][marker_about]: square markers with a black border, and with an arbitrary user-definable image in the interior. The "Hiro" marker used by default in the ARToolKit examples is an iconic example.

Multiple markers can be used to represent different objects or coordinate systems in an AR application. Additionally, a pattern can perform an important function in calculating the orientation of a square marker, since a pattern, being rotationally asymmetric, distinguishes between the four possible orientations of a marker in two dimensional space (the marker plane).

However, using arbitrary patterns inside a marker comes at some computational cost. The interior of every black square in the image captured from the camera must be compared against every known marker pattern at all four possible orientations. For a handful of markers, this computation comes at small cost, but as the number of markers in use in a single tracker rises to 20 or 100; the cost becomes significant. Additionally, pattern based markers are more likely to be confused by the tracker when there are a large number of markers (since there is a lower degree of uniqueness within the set of markers), leading to markers being misrepresented as each other.

The solution to the tracking difficulties caused by large number of markers is to use so-called two-dimensional barcode (2D-barcode) markers. These markers no longer have arbitrary user-defined patterns in the interior. Instead, they have a predetermined pattern of black and white squares in a simple grid arrangement (matrix pattern). ARToolKit treats the squares in a matrix pattern as a 2D-barcode; each unique matrix pattern being associated with an predetermined identifier.

2D-barcode markers are recognized in constant time meaning that different 2D-barcodes will take about the same amount of computer time to be recognized. Therefore, a large numbers of 2D-barcodes can be used in a scene at little additional computational cost. Additionally, when using 2D-barcode markers, there is a lower probability of one marker being mistaken for another. The downside is of course that the pattern inside the printed markers is no longer pictorial.

##Changing the Barcode Dimensions
The total number of possible barcodes available depends on the number of rows and columns in the barcode and the type of error detection and correction (EDC) algorithm enabled. Using better EDC will result in a smaller set of barcodes being available, but lower likelihood of markers being misrecognized during tracking.

The barcode type is set via the function [arSetMatrixCodeType][arSetMatrixCodeType]

The following table sets out the available number of barcodes:

| Matrix code type               | Maximum number of markers  | Hamming distance |
|--------------------------------|----------------------------|------------------|
| AR_MATRIX_CODE_3x3             | 64                         | 0                |
| AR_MATRIX_CODE_3x3_PARITY65    | 32                         | 1                |
| AR_MATRIX_CODE_3x3_HAMMING63   | 8                          | 3                |
| AR_MATRIX_CODE_4x4             | 8192                       | 0                |
| AR_MATRIX_CODE_4x4_BCH_13_9_3  | 512                        | 3                |
| AR_MATRIX_CODE_4x4_BCH_13_5_5  | 32                         | 5                |
| AR_MATRIX_CODE_5x5             | 4194304                    | 0                |
| AR_MATRIX_CODE_6x6             | 8589934592                 | 0                |

For example, the first row tells us that a 2D-barcode marker with a 3x3 matrix of squares yields 64 rotationally unique patterns that are associated with predetermined identifiers (IDs), but has no EDC capacity.

In general, it is better to use the barcode type with the greatest possible Hamming distance, as this results in the lowest likelihood of one marker being misrecognized as a different marker.

##2D-Barcode Markers as Multi-Markers
Multi-markers, not to be confused with the concept of multiple markers discussed above, are marker types that are made up of many sub-markers that are recognized and tracked as a single marker entity. This is opposed to recognizing and tracking multiple markers separately in a camera view. Patterns made up of a grid (matrix) of 2D-barcode markers are the default configuration for multi-marker sets, since they offer such radical performance improvements over other marker types with the use of multi-markers. Another advantage of multi-markers over traditional markers is that a multi-marker can still be recognized and tracked when some sub-markers are occluded from camera view.

The default barcode dimension for 2D-barcode markers in ARToolKit is a 3x3 pattern. For 3x3 2D-barcodes, there are 64 rotationally unique pattern arrangements making the marker suitable for augmented reality - enough patterns for most tabletop AR applications. You will find “.png” graphic files representing the 64 2D-barcode patterns in the ARToolKit SDK download; see folder path “[downloaded ARToolKit SDK]/doc/patterns/Matrix code 3x3 (72dpi)/”. These files can be printed.

The easiest way to use multi-markers in ARToolKit is to make a multi-marker dataset that consists of barcode markers. In order to do this, you only need to specify the number of markers, the ID of the barcodes involved, and their relative position to one another. For example, a single multi-marker dataset can be configured to track six unique sub-markers each affixed to six sides of a cube, allowing you to track a cube as a single object. This is done by defining a single multi-marker dataset that is configured with six sub-markers, the ID of the sub-markers (e.g. IDs 0–5), and where the sub-markers are relative to one another (rotationally and distance-wise). Due to the unique advantage multi-markers have for track-ability, the cube is still recognized and tracked despite the impossibility that all sides of a cube can be simultaneously in camera view.

For more information on multi-markers, including their configuration, visit the [multi-marker page][marker_multi].

[marker_about]: 3_Marker_Training:marker_about
[marker_multi]: 3_Marker_Training:marker_multi
[build_artoolkit]: 8_Advanced_Topics:build_artoolkit
[arSetMatrixCodeType]: http://www.artoolworks.com/support/doc/artoolkit5/apiref/ar_h/index.html#//apple_ref/c/func/arSetMatrixCodeType