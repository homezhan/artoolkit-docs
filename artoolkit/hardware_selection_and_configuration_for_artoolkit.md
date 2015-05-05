# Hardware Selection and Configuration For ARToolkit

## Camera selection for ARToolKit

Of the decisions facing the AR system designer, camera selection is perhaps the most critical, as it has a large bearing on the results achievable through subsequent image processing (e.g. by ARToolKit).

The ultimate goal of the imaging system (the camera lens, sensor and on-chip processing) is to provide maximum signal-to-noise ratio in any acquired image. This is because the image processing performed by ARToolKit and other similar systems involves mathematical correlation operations for identification. Noise has a high self-correlation, and thus the presence of noise appears requires a higher correlation for correct marker identification. This reduces the discriminative capacity of the system.

The key optical variables of interest to ARToolKit are the light-gathering power of the lens (primarily a factor its size), the camera aperture, and the sensor size. A larger lens and a larger physical sensor size are always desirable, so generally the choice of lens and sensor is determined primarily by cost and size constraints. Sensors on most consumer-level webcams are 1/4 inch CCD or CMOS sensors. More expensive cameras may increase the sensor size to 1/3 inch. High quality cameras designed for imaging applications will have sensor sizes of 1/2 inch or larger, but the price ratio from 1/4 inch to 1/2 inch can be 10x or more.

The camera aperture (the "shutter") is the third variable. Where the apeture is adjustable, opening it will allow more light onto the sensor, but this comes at the cost of depth-of-field. With the aperture wide open, objects at only a small range of depths will be in focus. If the aperture is closed down to a pinhole, all objects near and far will be in focus, but little light will reach the sensor, and thus pinhole apertures can only be used when external light conditions are very bright.

## Consumer webcams

### Logitech camera range

Logitech's cameras are a popular choice because of their relatively good quality/price ratio and their large range. The Quickcam range generally uses CMOS sensors, and the more expensive Quickcam Pro range CCD sensors. Drawbacks of Logitech cameras include poor driver support on non-Windows platforms, and brain-amputated model naming; in one cases, four radically different cameras produced over a period of 5 years have almost identical model names.

#### QuickCam Pro for Notebooks (Logitech part number 960-000057)

This is ARToolworks' recommended consumer level webcam. It has good imaging quality, a small form-factor, and acceptable field-of-view for AR applications.

[100px|left|thumb](/Image:Logitech_QuickCam_Pro_for_Notebooks_(960-000057)_front.png "wikilink")

<http://www.logitech.com/index.cfm/notebook_products/webcams/devices/3055&cl=hk,en>

## Professional imaging cameras

While consumer webcams provide satisfactory results in many types of AR application, for more demanding applications, professional camera equipment is in order.

Professional camera equipment offers the following advantages over consumer webcams:

- Control over optical parameters:

Particularly for optical tracking, it is important to be able to achieve a controlled balance between shutter speed (fast shutter reduces motion blur) and noise (in low light, increasing sensor gain amplifies the noise floor which can reduce recognition reliability). Most professional cameras offer controllable shutter speeds and gains.

- CCD imaging arrays:

Professional cameras generally contain quality CCD (charge-coupled device) imaging elements, which provide superior imaging quality over the CMOS sensors commonly deployed in consumer-grade equipment.

- Larger imaging elements:

1/2 inch CCDs used in pro cameras provide four times the light-gathering power of 1/4 inch CCDs used in consumer webcams. Additionally, they allow higher-resolution images even if using the same number of pixels.

- More imaging elements:

Most consumer level webcams provide 640x480 or smaller video streams, and ones that provide higher-resolutions may not be able to stream at these high resolutions, or may “fake” these higher resolutions by interpolation.

- Better connectivity:

Professional equipment typically uses high-bandwidth data buses, such as IEEE-1394 “Firewire” busses, which offer lower latency and greater throughput than USB2, as well as features such as daisy-chaining of multiple devices on one bus.

- Standard lens fittings and larger variety of lenses:

Professional cameras typically offer standardised fittings for lenses, such as c-mount, which allows fitting of simple variable focus, telephoto, wide angle, adjustable zoom, and variable aperture lenses, or even autofocus lenses.

### Point Grey camera range

The range of industrial cameras by Point Grey has become the de-facto standard for high-quality imaging in the AR application domain, thanks to their relatively low-cost, and flexibility. Point Grey cameras are supported in ARToolKit in the following ways:

-   Windows: The Point Grey WDM driver allows use of Point Grey cameras with the default WinDS video module, and the WinDSVL video input module, albeit without programmatic control of the parameters.
-   Windows: The ARToolKit WinDF video module connects directly to the FlyCapture SDK allowing complete control over all camera parameters.
-   Linux: The ARToolKit Linux Linux1394Cam video module has a variety of configuration options which support advanced features of Firewire (IEEE1394) cameras.'
-   Mac OS X: With a self-install install of [libdc1394](http://damien.douxchamps.net/ieee1394/libdc1394/) and a rebuild of the ARToolKit's libARvideo, the Linux1394Cam module can be used on Mac OS X.

#### Point Grey Firefly 2

This is an IEEE-1394 camera mounted in a steel housing, which accepts a variety of standard mini-mount lenses.

Image:Point Grey Firefly 2 (housing removed) - front.JPG Image:Point Grey Firefly 2 (housing removed) - rear.JPG

#### Point Grey Flea

This is an IEEE-1394 camera mounted in a steel housing, which accepts a variety of standard C-mount lenses.

Image:Point Grey Flea - front, no lens.JPG
Image:Point Grey Flea – rear, no lens.JPG
Image:Point Grey Flea - side view, no lens.JPG
Image:Point Grey Flea with manual focus variable aperture C-mount lens.JPG
Image:Point Grey Flea with manual focus variable aperture telephoto C-mount lens.JPG

## Further reading

Imaging systems are a fascinating and complex area. We highly recommend Edmund Industrial Optics' guide for background information and further reading in this area. <http://www.edmundoptics.com/technical-support/imaging/electronic-imaging-resource-guide/>