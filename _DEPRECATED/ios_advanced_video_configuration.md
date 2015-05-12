## Advanced - High-Resolution Image Capture
It is possible to capture a high-resolution image from the camera without closing the live video stream in ARToolKit. The photo that is captured uses the full photo resolution of the camera in use, and the size of this varies from device to device. The photo is always captured in portrait mode (taller than wide). Here are some example sizes:
-------------------------------- ------------------
iPad 3 (rear), iPhone 4 (rear)   1936x2592 pixels
iPhone 4s, iPhone 5 (rear)       2448x3264 pixels
iPad 2 (rear)                    960x720 pixels
-------------------------------- ------------------

The photo capture is initiated by invoking a method on the CameraVideo instance. In ARToolKit for iOS's ARViewController class, the CameraVideo instance is retrieved in the -start method:
<pre>
    // libARvideo on iPhone uses an underlying class called CameraVideo. Here, we
    // access the instance of this class to get/set some special types of information.
    CameraVideo *cameraVideo = ar2VideoGetNativeVideoInstanceiPhone(gVid->device.iPhone);
    if (!cameraVideo) {
        NSLog(@"Error: Unable to set up AR camera: missing CameraVideo instance.\n");
        [self stop];
        return;
    }
    // The camera will be started by -startRunLoop.
    [cameraVideo setTookPictureDelegate:self];
    [cameraVideo setTookPictureDelegateUserData:NULL];
</pre>

Before invoking the photo capture method, we must add a delegate method to the same class that receives delegate calls for incoming video frames. The delegate method is an optional member of the `\<CameraVideoTookPictureDelegate\>` protocol, cameravideoTookPictureHires:userData:jpegData:.

To this delegate method will be vended any user data set with `setTookPictureDelegateUserData:`, as well as a pointer to an NSData record holding the JPEG file. This file is suitable for writing to disk, or can alternately be saved to the user's photo roll.
<pre>
    - (void) cameravideoTookPictureHires:(id)sender userData:(void \*)data jpegData:(NSData \*)jpegData
    {
        if (![jpegData writeToFile:jpegPath atomically:NO]) {
            NSLog(@"Error writing captured photo to '%@'\n", jpegPath);
        }
    }
</pre>
or could be saved to the user's photo library:
<pre>
    import <AssetsLibrary/AssetsLibrary.h>
    
    - (void) cameravideoTookPictureHires:(id)sender userData:(void \*)data jpegData:(NSData \*)jpegData
    {
        ALAssetsLibrary *library = [[ALAssetsLibrary alloc] init];
        [library writeImageDataToSavedPhotosAlbum:jpegData metadata:nil completionBlock:^(NSURL *assetURL, NSError *error) {
            if (error) {
                NSLog(@"Error writing captured photo to photo album.\n");
            }
        }];
        [library release];
    }
</pre>

Finally, the actual CameraVideo method to invoke the capture operation can be called directly:
<pre>
    [cameraVideo capturePhoto];
</pre>

or can be registered (under an alternative name) as the receiver of an NSNotification, for example an ARViewTouchNotification vended by ARToolKit's default ARView class:
<pre>
    // Setup:
    [[NSNotificationCenter defaultCenter] addObserver:cameraVideo selector:@selector(capturePhotoNotification:) name:ARViewTouchNotification object:nil];
    // Removal of observer is required PRIOR to the CameraVideo instance being dealloc'ed:
    // Cleanup (done some time later):
    [[NSNotificationCenter defaultCenter] removeObserver:cameraVideo name:ARViewTouchNotification object:nil];
</pre>

### Notes
-   Photo capture will result in an interruption to video stream capture while the photo is captured and compressed to JPEG.
-   Photo capture may disrupt focus, exposure and white balance of the video stream capture.
-   A shutter sound plays during photo capture. This sound is played by the operating system, and cannot be disabled, although it will be silent if the device is muted.