# Upgrading an AR Application with the Latest ARToolkit for iOS Example Code

## Upgrading to ARToolKit for iOS release 27

There have been a significant number of internal changes in the ARMarker\* classes and the VirtualEnvironment/VEObject\* classes. Some external API has also changed.

### Changes in ARMarker\* and ARViewController

For ARMarker\* classes, structures required for tracking (e.g. AR3DHandle) are no longer passed to the ARMarker object at initialisation time, but at update time instead. The code in ARViewController that used to read:
<pre>
markers = [ARMarker newMarkersFromConfigDataFile:markerConfigDataFilename arHandle:gARHandle ar3DHandle:gAR3DHandle arPatternDetectionMode:&mode]
</pre>
should be replaced by:
<pre>
markers = [ARMarker newMarkersFromConfigDataFile:markerConfigDataFilename arPattHandle:gARPattHandle arPatternDetectionMode:&mode]
</pre>
and for NFT-only tracking, the code becomes:
<pre>
markers = [ARMarker newMarkersFromConfigDataFile:markerConfigDataFilename arPattHandle:NULL arPatternDetectionMode:NULL]
</pre>

Now, in the main processing loop (ARViewController -processFrame:) for square marker tracking, these lines:
<pre>
// Detect the markers in the video frame.
if (arDetectMarker(gARHandle, buffer->buff) < 0) return;
#ifdef DEBUG
NSLog(@"found %d marker(s).\n", gARHandle->marker_num);
#endif

// Update all marker objects with detected markers.
[markers makeObjectsPerformSelector:@selector(update)];
</pre>

must be replaced with these lines (for square marker tracking):

<pre>
// Detect the markers in the video frame.
if (arDetectMarker(gARHandle, buffer->buff) < 0) return;
int markerNum = arGetMarkerNum(gARHandle);
ARMarkerInfo *markerInfo = arGetMarker(gARHandle);

#ifdef DEBUG

NSLog(@"found %d marker(s).\n", markerNum);

#endif

// Update all marker objects with detected markers.
for (ARMarker *marker in markers) {
    if ([marker isKindOfClass:[ARMarkerSquare class]]) {
        [(ARMarkerSquare *)marker updateWithDetectedMarkers:markerInfo count:markerNum ar3DHandle:gAR3DHandle];
    } else if ([marker isKindOfClass:[ARMarkerMulti class]]) {
        [(ARMarkerMulti *)marker updateWithDetectedMarkers:markerInfo count:markerNum ar3DHandle:gAR3DHandle];
    } else {
        [marker update];
    }
}

</pre>

A similar modification is required for NFT tracking. See ARViewController.m in the ARAppNFT or ARAppNFTOSG examples.

### Changes in VirtualEnvironment and ARViewController

For the VirtualEnvironment class, the initialisation of the VirtualEnvironment has been separated from the act of adding objects to the environment from a config. file. So e.g. code in ARViewController.m that reads:

<pre>
// Set up the virtual environment.
self.virtualEnvironment = [[[VirtualEnvironment alloc] initWithObjectListFile:@"Data2/models.dat" arViewController:self] autorelease];
</pre>

should be replaced with:

<pre>
// Set up the virtual environment.
self.virtualEnvironment = [[[VirtualEnvironment alloc] initWithARViewController:self] autorelease];
[self.virtualEnvironment addObjectsFromObjectListFile:@"Data2/models.dat" connectToARMarkers:markers];
</pre>

### Using the new async video API

Release 27 changes the code for opening the video to use the new arVideoOpenAsync()/ar2VideoOpenAysnc() API. This offers improved performance and corrects a bug when re-opening the video.

Replace this code block in ARViewController:

<pre>
 
- (IBAction)start
{
// Open the video path.
char *vconf = "";
if (!(gVid = ar2VideoOpen(vconf))) {
NSLog(@"Error: Unable to open connection to camera.\n");
[self stop];
return;
}

</pre>

with:

<pre>

static void startCallback(void *userData);

- (IBAction)start
{
// Open the video path.
char *vconf = "";
if (!(gVid = ar2VideoOpenAsync(vconf, startCallback, self))) {
NSLog(@"Error: Unable to open connection to camera.\n");
[self stop];
return;
}

}

static void startCallback(void *userData) {

ARViewController *vc = (ARViewController *)userData;

[vc start2];

}

- (void) start2 {
</pre>

## Upgrading to ARToolKit for iOS release 15

iOS 6 changes the auto-rotation behaviour of view controllers. At present, the ARViewController supports portrait-mode only (although the view also looks fine at other orientations.) Add the following code to your ARViewController:

<pre> -
(NSUInteger)supportedInterfaceOrientations {

return UIInterfaceOrientationMaskPortrait;

}
</pre>

## Upgrading to ARToolKit for iOS release 13

Ensure that all UIWindow instances in .nib files have the "Fullscreen at launch" attribute selected to allow them to resize for different size devices.

[<File:ARToolKit4iOS> - UIWindow fullscreen at launch.png](/File:ARToolKit4iOS_-_UIWindow_fullscreen_at_launch.png "wikilink")

## Upgrading to ARToolKit for iOS release 12

The key change in ARToolKit for iOS release 12 is the shift caused by Apple's introduction of iOS 6.0 and the iPhone 5/iPod touch 5th Generation. Xcode 4.5 is required to build apps targeting iOS 6.0. At the same time, any app that targets iOS 6 may no longer target any release older than iOS 4.3. One of the underlying reasons for this change is that support has been dropped for the older ARMv6 CPU instruction set architecture (ISA), and with it the iPhone 3G. The 3GS and all later devices are capable of executing the ARMv7 ISA. The iPhone 5 also introduces a new ARMv7s ISA.

ARToolKit has been changed to match these requirements from Apple. All dependent libraries included in binary form are now built as ARMv7/ARMv7s fat binaries. Project settings have been changed to reflect the new minimum OS of iOS 4.3 and minimum Xcode version 4.5, and some support files have been added to support the new dimensions of the iPhone 5 and iPod touch 5th Generation.

Here are some of the changes in ARToolKit which you should carry into your own iOS projects:

1.  A new set of "Default" (launch) images has been supplied. Rather than being in the folder for each individual example app, these are now in a single folder named "ARToolworks Default images" inside the folder named "Xcode" at the root of the ARToolKit SDK. You will likely wish to replace these in your own projects with your own branding.
2.  Previously, ARViewController's -viewDidLoad method loaded an image named "Iris.png", and this image was visible while the waiting for the camera to become ready. A new better looking set of images has been supplied, including sizes for the iPad and iPhone 5-screen sizes. These new images must be included in your bundle resource:
    -   Iris@2x.png
    -   Iris-iPad.png
    -   Iris-iPad@2x.png
    -   Iris-568h@2x.png
        You'll also need to copy the new -viewDidLoad method into your own code.
3.  libARvideo has been updated to include calibration data for the iPhone 5.

## Upgrading from ARToolKit for iOS release 9 to release 10

ARToolKit for iOS release 10 simplifies handling of camera parameters. Rather than needing to bundle a large number of pre-supplied camera parameter files with your application, ARToolworks-produced camera parameters for all current iOS devices can be retrieved directly by a function call.

The new function prototypes are:

<pre>

int arVideoGetCParam(ARParam *cparam);
int ar2VideoGetCParam(AR2VideoParamT *vid, ARParam *cparam);

</pre>

cparam must be supplied; it is a pointer to an ARParam structure which will be filled out with the camera parameters. If no pre-supplied camera parameters are available (e.g. a new device comes to market) then the function returns 0, and you should load a default set of camera parameters yourself.

The previous function call:
<pre>
ar2VideoGetParams(gVid, AR_VIDEO_PARAM_IOS_RECOMMENDED_CPARAM_NAME, &cparam_name);
</pre>
is no longer supported. The ARViewController class and the example applications demonstrate the new approach. You must also change your code in your own applications as below:

Look for the following lines in ARViewController.m:

 <pre>

// Determine iOS device.
int device = -1;
ar2VideoGetParami(gVid, AR_VIDEO_PARAM_IOS_DEVICE, &device);

// If we have an iPhone 4 (with autofocus), tell arVideo what the typical focus distance will be.
// Note that this does NOT change the actual focus, it just lets arVideo make better recommendations
// for the camera parameter name (below).
if (device == AR_VIDEO_IOS_DEVICE_IPHONE4) {
ar2VideoSetParami(gVid, AR_VIDEO_PARAM_IOS_FOCUS, AR_VIDEO_IOS_FOCUS_0_3M); // Default is 0.3 metres. See `<AR/sys/videoiPhone.h>` for allowable values.
}

// Load the camera parameters, resize for the window and init.
char *cparam_name = NULL;
ar2VideoGetParams(gVid, AR_VIDEO_PARAM_IOS_RECOMMENDED_CPARAM_NAME, &cparam_name);
if (!cparam_name) cparam_name = "camera_para.dat";
ARParam    wparam;
chdir("Data2");
int ret = arParamLoad(cparam_name, 1, &wparam);
chdir("..");
if (ret < 0) {
NSLog(@"Error: Unable to load parameter file %s for camera.\n", cparam_name);
[self stop];
return;
}

</pre>

and replace the above lines with these:

<pre>

// Tell arVideo what the typical focal distance will be. Note that this does NOT
// change the actual focus, but on devices with non-fixed focus, it lets arVideo
// choose a better set of camera parameters.
ar2VideoSetParami(gVid, AR_VIDEO_PARAM_IOS_FOCUS, AR_VIDEO_IOS_FOCUS_0_3M); // Default is 0.3 metres. See `<AR/sys/videoiPhone.h>` for allowable values.

// Load the camera parameters, resize for the window and init.
ARParam wparam;
if (ar2VideoGetCParam(gVid, &wparam) < 0) {
char cparam_name[] = "Data2/camera_para.dat";
NSLog(@"Unable to automatically determine camera parameters. Using default.\n");
if (arParamLoad(cparam_name, 1, &wparam) < 0) {
    NSLog(@"Error: Unable to load parameter file %s for camera.\n", cparam_name);
    [self stop];
    return;
}
}

</pre>

Additionally, in the NFT examples, tracking parameters are now based on how many CPUs the devices provides. Replace the following block:

<pre>
if (device == AR_VIDEO_IOS_DEVICE_IPHONE3GS || device == AR_VIDEO_IOS_DEVICE_IPHONE4 || device == AR_VIDEO_IOS_DEVICE_IPODTOUCH4) {
// Settings for devices with single-core CPUs.
ar2SetTrackingThresh( ar2Handle, 5.0 );
ar2SetSimThresh( ar2Handle, 0.50 );
ar2SetSearchFeatureNum(ar2Handle, 10);
ar2SetSearchSize(ar2Handle, 24);
ar2SetTemplateSize1(ar2Handle, 4);
ar2SetTemplateSize2(ar2Handle, 4);
} else {
// Settings for devices with dual/multi-core CPUs, e.g. AR_VIDEO_IOS_DEVICE_IPAD2, AR_VIDEO_IOS_DEVICE_IPHONE4S, AR_VIDEO_IOS_DEVICE_IPAD3.
ar2SetTrackingThresh( ar2Handle, 5.0 );
ar2SetSimThresh( ar2Handle, 0.50 );
ar2SetSearchFeatureNum(ar2Handle, 16);
ar2SetSearchSize(ar2Handle, 24);
ar2SetTemplateSize1(ar2Handle, 6);
ar2SetTemplateSize2(ar2Handle, 6);
}

</pre>

with this block:

<pre>

if (threadGetCPU() <= 1) {

#ifdef DEBUG

NSLog(@"Using NFT tracking settings for a single CPU.");

#endif

ar2SetTrackingThresh( ar2Handle, 5.0 );
ar2SetSimThresh( ar2Handle, 0.50 );
ar2SetSearchFeatureNum(ar2Handle, 10);
ar2SetSearchSize(ar2Handle, 24);
ar2SetTemplateSize1(ar2Handle, 4);
ar2SetTemplateSize2(ar2Handle, 4);
} else {

#ifdef DEBUG

NSLog(@"Using NFT tracking settings for more than one CPU.");

#endif

ar2SetTrackingThresh( ar2Handle, 5.0 );
ar2SetSimThresh( ar2Handle, 0.50 );
ar2SetSearchFeatureNum(ar2Handle, 16);
ar2SetSearchSize(ar2Handle, 24);
ar2SetTemplateSize1(ar2Handle, 6);
ar2SetTemplateSize2(ar2Handle, 6);
}

</pre>

## Using FileMerge to merge changes in ARToolKit into your own code

One task developers of AR applications for iOS face is keeping track of changes with each release of ARToolKit for iOS release. For example, a change in the recommended way of calling an ARToolKit function may change from release of the software to another, due to changes in the underlying OS or ARToolKit itself, or to correct programming errors.

In each case, you would need to locate the change in the example code included with ARToolKit, and then make the same change in your own code in your own application.

If you have based your application's classes on the classes included with the example code in ARToolKit, you can use Apple's FileMerge tool to quickly locate the differences in a new ARToolKit release, and apply these to your own code. Here's how:

First, open FileMerge. It's included with Xcode Tools at path /Developer/Applications/Utilities/FileMerge.

Next, open a new "Compare files" window, and enlarge the window to show the extra fields labelled "Ancestor" and "Merge".

-   The "Left" box should be filled in with the version of the example code from the latest ARToolKit for iOS release.
-   The "Right" box should be filled in with the corresponding file from your own application.
-   The "Ancestor" box should be filled in with the same file from the previous ARToolKit for iOS release.
-   For an in-place merge, copy the path from the "Right" box to this box. To merge to a new file, enter a path.

Here is an example for a comparison of the ARViewController.m class between ARToolKit for iOS release 1.0, ARToolKit for iOS beta 2.1, and the ARViewController.m file in a fictional project called MyARProject.

[<File:Compare> files with ancestor example.png](/File:Compare_files_with_ancestor_example.png "wikilink")

The resulting compare files window allows you to see what changes were made in this file in the latest release, and to merge them into your own code. For example, here is the first change found. This shows that between beta 2.1 and release 1.0 of ARToolKit, the line "usingCoreVideo = FALSE;" was removed from the "-viewDidLoad" method of the ARViewController class. You would want to make the same change in your own version of this file.

[<File:Compare> files with ancestor example - result1.png](/File:Compare_files_with_ancestor_example_-_result_1.png "wikilink")