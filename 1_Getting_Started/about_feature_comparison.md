# ARToolKit Feature Comparison
ARToolKit v2.x and ARToolKit v5.x, while sharing a small subset of features, are vastly different. The latter represents nearly 8 years of further development of the former.

As well as obvious feature differences, the changes cover a wide variety of less obvious areas, including fundamental algorithms, internal design (modularity, reuse), optimization, external API design, connections to third-party systems, documentation and developer experience

##Natural Feature Tracking
Natural feature tracking is a major feature present in ARToolKit v5.x that is not present in v2.x

* Patented high-speed multi-resolution template-based tracker (libAR2)
* Feature-detector based surface recognition and tracking initializer (libKPM)
* Full suite of command-line tools, libraries, examples

##Tracking
* ICP pose estimator (vs. heuristic pose estimator in v2.x) with similar accuracy but 100x speed improvement.
* Variable square marker borders
* Variable square pictorial marker (template) resolution
* 2D barcode marker support
* Error detection and correction in barcode markers (BCH coding)
* Automatic binarization threshold selection for square tracking
* Pose estimate optimization using non-linear refinement
* Robust pose estimator using M-estimation
* Robust pose estimation from multi-square markers
* Pose filtering

##Tools Support
* Simple camera calibration based on OpenCV
* Web-based tools for barcode and NFT marker generation
* On-device camera calibration app for Android which feeds into a distributed camera calibration database
* Cloud-based distributed camera calibration database
* On-device optical/stereo-optical calibration app for Android
* New tools for square marker testing

##Stereo and Optical See-Through Support
* Support for simultaneous tracking from multiple video sources, e.g. stereo cameras
* Stereo camera calibration
* Robust pose estimation from calibrated stereo camera pairs
* Stereo rendering support
* Support for optical and stereo optical see-through displays on all platforms

##Video Input Focus
* Modular video input system (multiple video sources per platform, able to be selected at runtime)
* iOS video support
* Windows Media Foundation support
* Windows DirectShow support
* Windows FlyCapture SDK support (for Point Grey cameras)
* Windows DVCam support
* Windows QuickTime file/streaming support
* OS X QTKit support
* OS X QuickTime video file/streaming support
* JPEG sequence input module (e.g. from M-JPEG stream, or high-resolution images) support
* Linux/OSX lib1394 input support
* Android video support
* Support for high-resolution still-image capture during live tracking on iOS

##Mobile Focus
* Mobile-optimized (register size, memory usage)
* OpenGL ES and ES 2.x support
* Multi-platform mobile support
* Automatic provision of camera calibration for Apple iOS devices.
* Automatic provision of camera calibration data for Android devices via distributed camera calibration system
* Integration with GPS and compass (iOS)

##Optimization and Internals
* Full 64-bit support
* User-selectable floating point precision
* Hand-tuned ARM assembly in performance critical sections
* Optimized pathway for YUV video streams
* Multithreading used throughout

##New Languages and APIs
* C++
* Java (Android)
* Objective C (iOS, OS X)
* C#

##Graphics and Rendering
* Full support on all platforms for Unity 3D
* Full OpenSceneGraph support for advanced rendering
* Rendering of video from file or stream in-scene
* Support for chroma-keying of video streams

##Developer Experience
* Full support for latest developer environments, including Xcode 6.x for iOS and OS X, Visual Studio 2013 for Windows, and Eclipse for Android
* Vastly improved documentation, including new and improved reference documentation for over 350 API calls, as well as detailed guides and tutorials
