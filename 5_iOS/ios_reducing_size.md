#Reducing the Size of an iOS App
It is always desirable to minimize the size of any binary distribution when developing an iOS application, due to App Store cellular download limits.
The easiest way to inspect where your footprint is coming from is to inspect the package itself. Locate the built app, right-click on it, and choose "Show package contents".

![ARApp - Show package contents][show_package_contents]

Look at the file sizes in the resulting directory, and particularly at the size of the compiled executable and your data files (models etc.)

Here is a checklist of things you should check when trying to reduce the size of the executable:

-   If you do not need to support iOS devices running iOS versions older than 4.3, you can set `IOS_DEPLOYMENT_TARGET=4.3` in your application settings, and then set `ARCHS=armv7`. This will eliminate the armv6 architecture from the file, potentially cutting its size roughly in half.
-   Alternately, you can forgo the optimized armv7 architecture binary, and set `ARCHS=armv6 only`. [All iOS devices support the armv6 instruction set][ios_device_compatibility], and the performance loss may be very small.
-   Strip the binary of debugging and internal symbols (build settings `STRIP_INSTALLED_PRODUCT=YES`, `STRIP_STYLE=all`). Also, make sure that any embedded debug symbols are removed from copied binaries (build setting `COPY_PHASE_STRIP=YES`).
-   Make sure dead code (code which is defined but never called) is stripped. Check that build setting `DEAD_CODE_STRIPPING=YES`.

If trying to reduce the size of data files included with your application, pay particular attention to model files and textures.

-   Keep textures as small as possible. Some textures can be resized down to quite small sizes (e.g. 64x64 pixels) and still look acceptable, depending on usage and device. If your model format supports it, convert textures to compressed PVRTC format (Note: This is not supported by the glm model loader.).
-   Compress all sound files.
-   Reduce number of polygons in models.

[show_package_contents]: :arapp_-_show_package_contents.png
[ios_device_compatibility]:https://developer.apple.com/library/ios/documentation/DeviceInformation/Reference/iOSDeviceCompatibility/DeviceCompatibilityMatrix/DeviceCompatibilityMatrix.html
