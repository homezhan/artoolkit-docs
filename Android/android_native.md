#Android Native Development
The SDK package includes prebuilt native libraries. If you are not planning on altering any native code then you do not need to consult this section or install the Android NDK. On the other hand, if you want to implement part of your AR application in native code, then you will need to create a shared native library.

##Prerequisites
Building native static and shared ARToolKit libraries requires a development environment capable of building native Android libraries using the NDK. This necessarily requires an already working Android SDK environment.

*Note: This is by no means a comprehensive guide on how to setup an NDK development environment. If you need assistance in this area, please search online as there are many tutorials and articles covering this topic and it is outside the scope of this user guide.*

The following SDKs and tools should be installed and configured correctly. These are required for standard Android JDK development:

- [Java Development Kit][1]
- [Eclipse IDE][2]
- [Android SDK][3]
- [ADT Plugin for Eclipse][4]

and these extras are required for building native code with the NDK in Eclipse:

- CDT Plugin for Eclipse (install from within Eclipse).
- [Android NDK][5]
- [Android NDK plugin for Eclipse][6]

On Windows, NDK development is possible using [Cygwin][7], which provides a Linux-type environment. When installing Cygwin, ensure that the "make" package under "Devel" is selected, as this is required by the NDK and may not be installed by default.

Please ensure you have a working SDK and NDK environment before continuing.

##Building Native Libraries
Each native library in the SDK, whether core library or example, includes a Windows batch file called build.bat that automatically configures and initiates the build. The build.bat file first calls the SetNDKBuildVars.bat file in the SDK root directory. This batch file sets some environment variables that are required for the build process, including the paths to the various tools and SDKs listed above. Naturally, these paths will differ from machine to machine, so it is important to edit this file to match the current development environment. Until this file has been configured, an error message will appear, as shown below.

![set_ndk_build_vars][set_ndk_build_vars]

Simply edit the file in a text editor, following the instructions in the comments within the file.

You can now execute the build.bat file for one of the native libraries, such as [ARToolKitWrapper][android_developing]: `ARToolKitWrapper/android/build.bat`

The NDK tools will now start building the ARToolKitWrapper library. Since it depends on ARToolKit, those static libraries will also be built. The build process will run twice, as the library is built for two different platform architectures. This is normal.

![set_ndk_build][set_ndk_build]

When the build completes, there will be new shared libraries in `ARToolKitWrapper/android/libs`.

To use this native library in your own Android application, you will need to copy the libs directory to your Android application project directory. ![right][libs_directory]

[1]: http://www.oracle.com/technetwork/java/javase/downloads/index.html
[2]: http://www.eclipse.org/
[3]: http://developer.android.com/sdk/index.html
[4]: http://developer.android.com/sdk/eclipse-adt.html
[5]: http://developer.android.com/sdk/ndk/index.html
[6]: http://tools.android.com/recent/usingthendkplugin
[7]: http://www.cygwin.com
[android_developing]: Android:android_developing

[set_ndk_build_vars]: /set_ndk_build_vars.png
[set_ndk_build]: /set_ndk_build.png
[libs_directory]: /libs_directory.png