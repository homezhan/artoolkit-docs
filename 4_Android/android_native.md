#Android Native Development
The ARToolKit SDK package and the git cloned GitHub local repository of "artoolkit5" includes prebuilt native libraries. It's advised that a local repository be used since downloaded package are rarely up-to-date. If you are not planning on altering any native code then you do not need to consult this section or install the Android NDK. On the other hand, if you want to implement part of your AR application in native code, then you will need to ARToolKit native C/C++ dependencies.

##Prerequisites
Building native ARToolKit dependencies, the static, shared and, specifically, ARWrapper (the C programming language application binary interface, ABI, to the ARToolKit functionality) libraries, requires a development environment capable of building libraries native to Android using the Android NDK. Currently, ARToolKit for Android development actively supports the development systems of Mac OS X 9+ and Windows Desktop 8.1 and 10. However, there are those in the ARToolKit community who have successfully developed using Linux.

*Note: This is by no means a comprehensive guide on how to setup an NDK development environment. If you need assistance in this area, please search online as there are many tutorials and articles covering this topic and it is outside the scope of this user guide.*

The following SDKs and tools should be installed and configured correctly one of the chosen supported development systems. These are required for standard Android JDK development:

- [Java Development Kit][1]
- [Android SDK][2] 
<p style="margin-left: 2em;">Downloaded with Android Studio IDE to</p>
<p style="margin-left: 4em;">for Mac OS X:</p>
<p style="margin-left: 6em;">default: *"/Users/&lt;user&gt;/Library/Android/sdk"*</p>
<p style="margin-left: 4em;">for Windows Desktop:</p>
<p style="margin-left: 6em;">recommended: *"C:\Users\\&lt;user&gt;\\Android\\sdk"*</p>
- [Android Studio IDE][3] - version 1.5.x
- [Eclipse IDE][4] - deprecated
- [ADT Plugin for Eclipse][5] - deprecated

Requirements for building native code with the NDK within or outside of the Android Studio IDE. Eclipse usage is deprecated:

- [Android NDK Preview][6] (NDK downloaded by and works with the Android Studio IDE)
- [Git distributed version control system and Git bash][7] (requirement for Windows Desktop, optional for Mac OS X)
- ADT Plugin for Eclipse (install from within Eclipse) - deprecated
- Android NDK plugin for Eclipse - deprecated
- Cygwin (requirement only for Android development on Windows Desktop) - deprecated, replaced by Git bash.

---

####Regarding the Windows Desktop development environment

Some Unix commands are required by the Android NDK's ndk-build.cmd script to work. These commands are provided by the Git download (integrated with the Git bash shell). And since Git is usually required for GitHub repository interaction, thankfully, Cygwin, that provides a Unix-like environment over Windows, can be replaced by the Git bash provided environment. Cygwin is fairly large and invasive and the installation setup is confusing. Therefore, Cygwin seems an overkill for the  requirements of the Windows' ndk-build.cmd script.

#####Special Git installation instructions for Windows Desktop only

In the Git setup wizard:

- Accept the default selected components
- For the "Adjusting your PATH environment" step, select the default "Use Git only"
- For the "Configuring the line ending conversions" step, select the default "Checkout Windows-style, commit Unix-style line ends"

---

Please ensure you have a working Android SDK and NDK environment before continuing.

To help with the Eclipse to Android Studio IDE transition, in the GitHub "artookit5" repository, see the [document][8]:<br/>"\<repo root\>/AndroidStudioProjects/Docs/AS_Migration.pdf."

##Building Native Android Libraries
To build using the Android NDK toolchain, placed in the downloaded NDK is a script file, for Mac OS X, named "ndk-build" or, for Windows Desktop, named "ndk-build.cmd." This script file is placed directly under the root folder of the downloaded NDK. The NDK root folder name is defaulted by Android Studio as "ndk-bundle." Therefore, the first step is to set some environment variables for both Mac OS X and Windows Desktop. For Windows Desktop, the following can be defined as Windows system environment variables or exported by the Git bash shell's ".bash_profile" file.

* Set ANDROID_HOME to indicate the path to root folder of the downloaded Android SDK.
* Set NDK to indicate the path to root folder (most likely, "ndk-bundle") of the downloaded NDK.
* Set PATH to include a path to the ndk-build\[.cmd\] script file, the root folder of the downloaded NDK. The NDK environment variable can be used here.

Then, for both Mac OS X and Windows Desktop, re-source the command-line shell so that updated environment variables are seen by the subsequent command-line shell. 

Next, proceed to the "android" folder directly off the root folder of the ARToolKit SDK or local repository. There are two script files that are used on both the Mac OS X and Windows Desktop development environments:

* build.sh - builds ARToolKit Android native C/C++ binaries for several Android ABIs
* build_native_examples.sh - builds those ARToolKit Android Studio example app projects that contain both native C/C++ and Java source code, again, for several Android ABIs

Both scripts utilize the Android NDK and toolchain through the ndk-build script.

To build, from the bash command-line (for Windows Desktop, this will be the Git bash shell), execute the "./build.sh" script file, without arguments. When "build.sh" completes without errors, there will be dependencies built for several Android ABIs here: 

* Mac OS X: &lt;ARTK SDK or repo root&gt;android/*libs*
* Windows Desktop: C:\\&lt;ARTK SDK or repo root&gt;\\android\\*libs*

These are the ARToolKit binaries built for the various Android ABIs. The Android Studio example projects, that don't include native C/C++ source code, are populated with the content of the generated *libs* folder.

To build the Android Studio example app projects that do include native C/C++ source code and to build the project's C/C++ source, after executing the "./build" script file, execute "./build_native_examples.sh", without arguments. When "build_native_examples.sh" script completes without errors, the native Android Studio example projects are populated with the content of the generated *libs* folder. Using an actual example Android Studio project, "ARSimpleNativeProj," the *libs* folder is copied here:

<div style="margin-left: 2em;">
<p>&lt;ARTK SDK or repo root&gt;/<br/>
AndroidStudioProjects/ARSimpleNativeProj/aRSimpleNative/src/main/
</p>
</div>

Once the native dependencies are built and copied, open an Android Studio example project and build the project's Java source files. If all builds, deploy to an Android simulated device or a *real* development device.

To use the native ARToolKit binaries in your own Android application, you will need to copy the *libs* folder generated by the "build.sh" script to your Android application project folder using the following project offset:

<p style="margin-left: 2em;">
 &lt;Android Studio Project&gt;/&lt;module&gt;/src/main
</p>

---

####Note

We realize we're have not fully integrated the build process from within the Android Studio IDE. This is partly because NDK development support is not seamlessly integrated into Android Studio as of yet. Just know that it is our goal and we are working on it.

---

[1]: http://www.oracle.com/technetwork/java/javase/downloads/index.html
[2]: http://developer.android.com/sdk/index.html
[3]: http://developer.android.com/sdk/index.html
[4]: http://www.eclipse.org/
[5]: http://developer.android.com/sdk/eclipse-adt.html
[6]: http://tools.android.com/tech-docs/android-ndk-preview
[7]: https://git-scm.com
[8]: https://github.com/artoolkit/artoolkit5/blob/master/AndroidStudioProjects/Docs/AS_Migration.pdf

[android_developing]: 4_Android:android_developing