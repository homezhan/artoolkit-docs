# ARToolkit Feature Comparison

<table border="1" cellspacing="0">
<caption>ARToolKit v2.x vs ARToolKit Professional v4.x feature comparison
</caption>
<tbody><tr>
<td>
</td><td><b>ARToolKit v2.x</b>
</td><td><b>ARToolKit v5.x (Desktop)</b>
</td><td><b>ARToolKit v5.x (iOS)</b>
</td><td><b>ARToolKit v5.x (Android)</b>
</td></tr>
<tr>
<td>Platform support
</td><td>Windows, Linux, OS X
</td><td>Windows XP SP 3-, Linux, OS X 10.5-
</td><td>iOS v4.3-
</td><td>Android 2.2-
</td></tr>
<tr>
<td colspan="5">&nbsp;
</td></tr>
<tr>
<td colspan="5"><b>64-bit support</b>
</td></tr>
<tr>
<td>x86-64	</td><td>x	</td><td>x	</td><td>.	</td><td>.
</td></tr>
<tr>
<td>PowerPC G5	</td><td>x	</td><td>x	</td><td>.	</td><td>.
</td></tr>
<tr>
<td>IA64	</td><td>.	</td><td>.	</td><td>.	</td><td>.
</td></tr>
<tr>
<td>ARM64 (ARM AArch64)	</td><td>.	</td><td>.	</td><td>x	</td><td>x
</td></tr>
<tr>
<th colspan="5">&nbsp;
</th></tr>
<tr>
<td>USB webcam input	</td><td>x	</td><td>x	</td><td>.	</td><td>.
</td></tr>
<tr>
<td>DV video input	</td><td>x	</td><td>x	</td><td>.	</td><td>.
</td></tr>
<tr>
<td>IIDC firewire video input	</td><td>x	</td><td>x	</td><td>.	</td><td>.
</td></tr>
<tr>
<td>AVI file video streaming	</td><td>x	</td><td>x	</td><td>.	</td><td>.
</td></tr>
<tr>
<td>QuickTime/MP4 video streaming from file	</td><td>.	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>QuickTime/MP4 video streaming from network	</td><td>.	</td><td>x	</td><td>.	</td><td>.
</td></tr>
<tr>
<td>Multiple video streams supported	</td><td>x	</td><td>x	</td><td>x	</td><td>.
</td></tr>
<tr>
<td>Video input type able to be changed at runtime	</td><td>.	</td><td>x	</td><td>x	</td><td>.
</td></tr>
<tr>
<td>Multiple video streams from different sources	</td><td>.	</td><td>x	</td><td>x	</td><td>.
</td></tr>
<tr>
<td colspan="5">&nbsp;
</td></tr>
<tr>
<td>RGB pixel format support	</td><td>x	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>Grayscale pixel format	</td><td>.	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>YUV pixel formats	</td><td>x	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>Packed pixel formats	</td><td>.	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td colspan="5">&nbsp;
</td></tr>
<tr>
<td>Kato's heuristic pose estimator	</td><td>x	</td><td>.	</td><td>.	</td><td>.
</td></tr>
<tr>
<td>Pose estimate optimization using non-linear refinement	</td><td>.	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>Robust pose estimator using M-estimation	</td><td>.	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>Support for stereo pose estimation	</td><td>.	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>Filtering of continuous pose estimates	</td><td>x (1)	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td colspan="5">&nbsp;
</td></tr>
<tr>
<td>Pinhole lens model	</td><td>x	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>Pinhole lens model with pixel aspect ratio	</td><td>.	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>OpenCV lens models with scale factor supported	</td><td>.	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>Rapid OpenCV-based camera calibration	</td><td>.	</td><td>x	</td><td>.	</td><td>x
</td></tr>
<tr>
<td>Stereo video calibration	</td><td>.	</td><td>x	</td><td>.	</td><td>.
</td></tr>
<tr>
<td colspan="5">&nbsp;
</td></tr>
<tr>
<td>Automatic binarization threshold selection	</td><td>.	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>Tracking from interlaced sources	</td><td>x	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>Simultaneous tracking of multiple camera views	</td><td>x (1)	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>Pictorial (template) markers	</td><td>x	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>2D-barcode markers	</td><td>.	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>Marker border width variable at runtime	</td><td>.	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>Barcode marker error detection and correction </td><td>.	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td colspan="5">&nbsp;
</td></tr>
<tr>
<td colspan="5"><b>Rendering support</b>
</td></tr>
<tr>
<td>OpenGL	</td><td>x	</td><td>x	</td><td>.	</td><td>.
</td></tr>
<tr>
<td>OpenGL ES	</td><td>.	</td><td>.	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>OpenGL ES 2.0	</td><td>.	</td><td>.	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>OpenVRML	</td><td>x	</td><td>x	</td><td>.	</td><td>.
</td></tr>
<tr>
<td>OpenSceneGraph	</td><td>x (2)	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>DirectX	</td><td>.	</td><td>.	</td><td>.	</td><td>.
</td></tr>
<tr>
<td>Unity 3D	</td><td>.	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td colspan="5">&nbsp;
</td></tr>
<tr>
<td colspan="5"><b>Language bindings</b>
</td></tr>
<tr>
<td>C	</td><td>x	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>C (OO)/C++	</td><td>.	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td>Objective-C	</td><td>.	</td><td>x	</td><td>x	</td><td>.
</td></tr>
<tr>
<td>Java	</td><td>x	</td><td>x (3)	</td><td>.	</td><td>x
</td></tr>
<tr>
<td>C#	</td><td>.	</td><td>x (3)(4)	</td><td>. (4)	</td><td>. (4)
</td></tr>
<tr>
<td>Flash AS3 </td><td>.	</td><td>x (3)	</td><td>.	</td><td>.
</td></tr>
<tr>
<td>Proce55ing </td><td>.	</td><td>x (3)	</td><td>.	</td><td>.
</td></tr>
<tr>
<td>MATLAB	</td><td>x	</td><td>.	</td><td>.	</td><td>.
</td></tr>
<tr>
<td>SilverLight	</td><td>.	</td><td>x (3)	</td><td>.	</td><td>.
</td></tr>
<tr>
<td colspan="5">&nbsp;
</td></tr>
<tr>
<td colspan="5"><b>Licensing</b>
</td></tr>
<tr>
<td>Open source license, GPLv2 compatible	</td><td>x	</td><td>.	</td><td>.	</td><td>.
</td></tr>
<tr>
<td>Commercial license possible	</td><td>.	</td><td>x	</td><td>x	</td><td>x
</td></tr>
<tr>
<td colspan="5">&nbsp;
</td></tr>
<tr>
<td colspan="5"><b>Notes</b>
</td></tr>
<tr>
<td colspan="5">(1) Multiple tracking instances possible only when pose estimate filtering is disabled.
</td></tr>
<tr>
<td colspan="5">(2) Via osgART
</td></tr>
<tr>
<td colspan="5">(3) Via FLARToolKit/NyARToolKit/SLARToolKit
</td></tr>
<tr>
<td colspan="5">(4) Also supported via ARToolKit for Unity
</td></tr></tbody></table>