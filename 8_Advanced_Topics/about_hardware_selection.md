#Hardware Selection and Configuration

##A Note on Camera Selection
Of the decisions facing the AR system designer, camera selection is perhaps the most critical, as it has a large bearing on the results achievable through subsequent image processing (e.g. by ARToolKit).

The ultimate goal of the imaging system (the camera lens, sensor and on-chip processing) is to provide maximum signal-to-noise ratio in any acquired image. This is because the image processing performed by ARToolKit and other similar systems involves mathematical correlation operations for identification. Noise has a high self-correlation, and thus the presence of noise requires a higher correlation for correct marker identification. This reduces the discriminative capacity of the system.

The key optical variables of interest to ARToolKit are the light-gathering power of the lens (primarily a factor of its size), the camera aperture, and the sensor size. A larger lens and a larger physical sensor size are always desirable, so generally the choice of lens and sensor is determined primarily by cost and size constraints. Sensors on most consumer-level webcams are 1/4 inch CCD or CMOS sensors. More expensive cameras may increase the sensor size to 1/3 inch. High quality cameras designed for imaging applications will have sensor sizes of 1/2 inch or larger, but the price ratio from 1/4 inch to 1/2 inch can be 10x or more.

The camera aperture (the "shutter") is the third variable. Where the aperture is adjustable, opening it will allow more light onto the sensor, but this comes at the cost of depth-of-field. With the aperture wide open, objects at only a small range of depths will be in focus. If the aperture is closed down to a pinhole, all objects near and far will be in focus, but little light will reach the sensor, and thus pinhole apertures can only be used when external light conditions are very bright.

##Consumer Webcams

### Logitech Cameras
Logitech's cameras are a popular choice because of their relatively good quality/price ratio and their large range. The Quickcam range generally uses CMOS sensors, and the more expensive Quickcam Pro range, CCD sensors. Drawbacks of Logitech cameras include poor driver support on non-Windows platforms, and brain-amputated model naming; in one case, four radically different cameras produced over a period of 5 years have almost identical model names.

## Professional Imaging Cameras
While consumer webcams provide satisfactory results in many types of AR application, for more demanding applications, professional camera equipment is in order. Professional camera equipment offers the following advantages over consumer webcams:

###Control over Optical Parameters
Particularly for optical tracking, it is important to be able to achieve a controlled balance between shutter speed (fast shutter reduces motion blur) and noise (in low light, increasing sensor gain amplifies the noise floor which can reduce recognition reliability). Most professional cameras offer controllable shutter speeds and gains.

###CCD Imaging Arrays
Professional cameras generally contain high quality CCD (charge-coupled device) imaging elements, which provide superior imaging quality over the CMOS sensors commonly deployed in consumer-grade equipment.

###Larger Imaging Elements
1/2 inch CCDs used in pro cameras provide four times the light-gathering power of 1/4 inch CCDs used in consumer webcams. Additionally, they allow higher-resolution images even if using the same number of pixels.

###More Imaging Elements
Most consumer level webcams provide 640x480 or smaller video streams, and ones that provide higher-resolutions may not be able to stream at these high resolutions, or may “fake” these higher resolutions by interpolation.

###Better Connectivity
Professional equipment typically uses high-bandwidth data buses, such as IEEE-1394 “Firewire” busses, which offer lower latency and greater throughput than USB2, as well as features such as daisy-chaining of multiple devices on one bus.

###Standard Lens Fittings - More Lens Variety
Professional cameras typically offer standardized fittings for lenses, such as c-mount, which allows fitting of simple variable focus, telephoto, wide angle, adjustable zoom, and variable aperture lenses, or even autofocus lenses.

###Point Grey Cameras
The range of industrial cameras by Point Grey has become the de-facto standard for high-quality imaging in the AR application domain, thanks to their relatively low-cost, and flexibility. Point Grey cameras are supported in ARToolKit in the following ways:

-   Windows: The Point Grey WDM driver allows use of Point Grey cameras with the default WinDS video module, and the WinDSVL video input module, albeit without programmatic control of the parameters.
-   Windows: The ARToolKit WinDF video module connects directly to the FlyCapture SDK allowing complete control over all camera parameters.
-   Linux: The ARToolKit Linux Linux1394Cam video module has a variety of configuration options that support advanced features of Firewire (IEEE1394) cameras.'
-   Mac OS X: With a self-install install of [libdc1394][1] and a rebuild of the ARToolKit's libARvideo, the Linux1394Cam module can be used on Mac OS X.

#### Point Grey Firefly 2
This is an IEEE-1394 camera mounted in a steel housing, which accepts a variety of standard mini-mount lenses.

![Point Grey Firefly 2 (housing removed) - front][point_grey_housing_removed_front]
![Point Grey Firefly 2 (housing removed) - rear][point_grey_housing_removed_rear]

#### Point Grey Flea
This is an IEEE-1394 camera mounted in a steel housing, which accepts a variety of standard C-mount lenses.

![Point Grey Flea - front, no lens][point_grey_flea_front_no_lens]
![Point Grey Flea - rear, no lens][point_grey_flea_rear_no_lens]
![Point Grey Flea - side view, no lens][point_grey_flea_side_no_lens]
![Point Grey Flea with manual focus variable aperture C-mount lens][point_grey_flea_manual_variable]
![Point Grey Flea with manual focus variable aperture telephoto C-mount lens][point_grey_flea_manual_telephoto]

## Further reading
Imaging systems are a fascinating and complex area. We highly recommend [Edmund Industrial Optics'][2] guide for background information and further reading in this area.

[1]: http://damien.douxchamps.net/ieee1394/libdc1394/
[2]: http://www.edmundoptics.com/capabilities/imaging-optics/imaging-resource-guide/

[point_grey_housing_removed_front]: https://github.com/artoolkit/artoolkit-docs/tree/master/_media/point_grey_firefly_2_housing_removed_-_front.jpg
[point_grey_housing_removed_rear]: https://github.com/artoolkit/artoolkit-docs/tree/master/_media/point_grey_firefly_2_housing_removed_-_rear.jpg
[point_grey_flea_front_no_lens]: https://github.com/artoolkit/artoolkit-docs/tree/master/_media/point_grey_flea_-_front_no_lens.jpg
[point_grey_flea_rear_no_lens]: https://github.com/artoolkit/artoolkit-docs/tree/master/_media/point_grey_flea_rear_no_lens.jpg
[point_grey_flea_side_no_lens]: https://github.com/artoolkit/artoolkit-docs/tree/master/_media/point_grey_flea_-_side_view_no_lens.jpg
[point_grey_flea_manual_variable]: https://github.com/artoolkit/artoolkit-docs/tree/master/_media/point_grey_flea_with_manual_focus_variable_aperture_c-mount_lens.jpg
[point_grey_flea_manual_telephoto]: https://github.com/artoolkit/artoolkit-docs/tree/master/_media/point_grey_flea_with_manual_focus_variable_aperture_telephoto_c-mount_lens.jpg
