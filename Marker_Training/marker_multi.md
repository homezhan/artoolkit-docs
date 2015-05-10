# Multimarker Tracking
In ARToolKit the term *multimarker* (as a single word) has a special meaning. Rather than meaning the use of more than one marker at a time, it refers specifically to the use of multiple square markers fixed to a single object. Multimarker tracking has special support in the ARToolKit API and allows for a number of tracking performance and stability enhancements.

In multimarker tracking, the markers can have arbitrary relationships to each other, but these relationships must remain fixed. In practise, the most common multimarker arrangement is multiple markers on a single flat sheet, as in the examples provided with ARToolKit:
![4x3 (lower) and 8x6 (upper) barcode multimarker examples.][Example_multimarker_barcode]

Many other useful arrangements are possible, e.g. the cube example also provided with ARToolKit:
![The printed, and assembled cube example. This cube works with the multiCube example in ARToolKit for Desktop.][Example_multimarker_cube]

Some of the benefits of multimarkers include:

-   Increased robustness to occlusion: even when one marker is obscured, another may be visible.
-   Improved pose-estimation accuracy: in a multimarker set, all marker corners are used to calculate the pose, meaning that the markers effectively cover a larger optical angle, resulting in reduced numerical error.
-   Possibility for robust pose estimation (using M-estimation). With multimarker tracking, statistical techniques can be applied to improve rejection of mis-read marker poses.

Note that these are the same advantages of using NFT (texture) tracking. The advantages of multimarker tracking over NFT is that it is less CPU intensive, faster, and can operate reliably at greater distances from the camera. The obvious disadvantage is that it requires the surface to be covered in square markers.

## Barcode (Matrix) vs Pictorial (Template) Multimarkers
The examples shown above all use [barcode (matrix) markers][marker_barcode]. [Pictorial (template) markers][marker_about] can also be used, and ARToolKit has included an example:
![This example uses six pattern (template) markers. The multimarker config and its pattern files can be found in the bin/Data/multi directory of the SDK. This works with the multi example in ARToolKit for Desktop][Example_multimarker_template]

Barcode markers do have the advantage over pictorial markers of speed, setup simplicity (no need to make pattern files) and improved rejection of false matches when using markers with error detection and correction (e.g. the marker sets with Hamming codes).

## Built-in support in examples for multimarker tracking
ARToolKit for Desktop includes the following examples of multimarker tracking:
-   multi
-   multiCube

PDF files you can print out for the marker sets used in these examples can be found in the files `doc/patterns/Multi pattern (template, A4).pdf` or `doc/patterns/Multi pattern (template, Letter).pdf` and `doc/patterns/Cubes/cube00-05-a4.pdf` or `doc/patterns/Cubes/cube00-05-letter.pdf`. If you print on ISO A4 size, choose the PDF with "A4" in the name, or if you print on US Letter size paper, choose the PDF with "Letter" in the name.

In ARToolKit for iOS, any app using the ARAppCore code supports multimarker tracking without any further work by the developer. The code is provided in the ARMarkerMulti Obj-C class. Thus, the following examples include support for multimarker tracking, as well as other markers types:

-   ARApp2
-   ARAppOSG
-   ARAppMovie

In ARToolKit for Android, any app using the ARBaseLib library or its underlying native implementation, ARWrapper, supports multimarker tracking without any further work by the developer. The code is provided in the ARMarkerMulti C++ class. Thus, the following examples include support for multimarker tracking, as well as other markers types:

-   ARSimple
-   ARSimpleInteraction
-   ARSimpleNative
-   ARSimpleNativeCars

## Multimarker Configuration
In all the examples, multimarkers are specified to the system by use of a multimarker configuration file. This is a plain text file with a structure which sets out the number of markers, their barcode IDs or pattern file names, and their relationship to a common shared coordinate system origin.

A multimarker configuration file is structured as follows:

-   Lines beginning with a \# character are treated as comments and ignored.
-   Blank lines are ignored. Blank lines do not play any part in the configuration structure.
-   The first non-blank/comment line in the file must be a single integer specifying the number of markers to be read from the multimarker configuration file. (This will usually be the actual number of markers in the set.)
-   Each five subsequent non-blank/comment lines specify a single marker in the set,
    -   The first line of each marker specification is either an integer greater than or equal to 0 (if using barcode markers) or the path to a pictorial (template) marker pattern file, expressed relative to this multimarker configuration.
    -   The next line specifies the size of this marker. Usually this will be the width of the outer border in millimetres. (Multiply inches by 25.4 to get millimetres).
    -   The last three lines of the marker specification are the first three rows of a standard 4x4 homogenous coordinate transform matrix (in row-major order). This transform is from the combined multimarker set's coordinate system origin to the origin of this marker. More information on this transform is set out below.

###Example
If we examine the first marker definition in the example multimarker set bin/Data/cubeMarkerConfig.dat, we see these lines:
<pre>
    \#marker 1
    00
    40.0
    1.0000  0.0000  0.0000    0.0000
    0.0000  1.0000  0.0000    0.0000
    0.0000  0.0000  1.0000    0.0000
</pre>

Following the above guide, we see that this uses barcode pattern 0 and the marker is 40 mm wide. The transformation matrix is the identity matrix, i.e. marker 0's origin is co-located with the origin of the multimarker set, and the axes are the co-aligned.

###Transformation Matrices for Markers in a Set
If we consider the transformation matrix of individual markers, the first three columns are a rotation matrix which represent the rotation of the marker with respect to the origin of the multimarker set. This is the standard 3x3 rotation matrix familiar in computer graphics or linear algebra. The fourth column is the offset from the origin of the multimarker set to the origin (the centre) of this the individual marker.

So for example, if marker 0 in the example was rotated by angle theta about the X axis then the matrix would change to:
<pre>
    1.0000 0.0000 0.0000 0.0000
    0.0000 cos(theta) -sin(theta) 0.0000
    0.0000 sin(theta) cos(theta) 0.0000
</pre>

As a further example, consider marker 01 in the cube example. Its definition is:
<pre>
    \#marker 2
    01
    40.0
    1.0000  0.0000  0.0000    0.0000
    0.0000  0.0000  1.0000   30.0000
    0.0000 -1.0000  0.0000  -30.0000
</pre>

This tells us that the origin of marker 01 is offset +30 mm in the direction of the multimarker set's y axis, and -30 mm in the direction of the multimarker set's z axis. Finally, it is rotated by -90 degrees (in a right-hand sense) around the multimarker set's positive x axis.

####A Mathematical Explination
Let `R[1-0]` be a 4x4 matrix where the first three rows are the values specified in configuration file, and the fourth row is the row vector `{0, 0, 0, 1}`. Then when `R[1-0]` is applied to a point vector in the marker coordinate system `p[1]`, it transforms it into a point vector expressed in the multimarker coordinate system `p[0]`, i.e. `p[0] = R[1-0] • p[1]` (where • is the normal matrix multiplication operator).

####A Visual Explination
In the image below, the red arrows denote the x, y and z axes of the multimarker coordinate system, aligned with marker 0. The blue arrows denote unit vectors `n̂``, `ô` and `â`, aligned with the `x`, `y`, and `z` axes of the marker 1 coordinate system. The green arrow denotes `p`, a vector extending from the origin of the multimarker coordinate system to the origin of of the marker 1 coordinate system. The transform matrix for marker 1 can then be considered 4 column vectors expressing the projection of `n̂``, `ô`, `â` and `p` onto `x`, `y`, and `z`.

The matrix is thus:
<pre>
    n[x] o[x] a[x] p[x]
    n[y] o[y] a[y] p[y]
    n[z] o[z] a[z] p[z]
</pre>

Compare this to the example above, and it can be seen that for marker 01 on the cube, `n̂`` is aligned with the `x` axis (no change), `ô` points completely in the direction of `-z`, and `â` points completely in the direction of `+y`.

![Cube marker axes][Cube_marker_axes]

[marker_about]: Marker_Training:marker_about
[marker_barcode]: Marker_Training:marker_barcode
[Example_multimarker_barcode]: /Example_multimarker_barcode.jpg
[Example_multimarker_cube]: /Example_multimarker_cube.jpg
[Example_multimarker_template]: /Example_multimarker_template.jpg
[Cube_marker_axes]: /Cube_marker_axes.png