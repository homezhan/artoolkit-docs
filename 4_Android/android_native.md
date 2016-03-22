#Android Native Development
The ARToolKit SDK package and the git cloned GitHub local repository of "artoolkit5" includes prebuilt native libraries. It's advised that a local repository be used since downloaded package are rarely up-to-date. If you are not planning on altering any native code then you do not need to consult this section or install the Android NDK. On the other hand, if you want to implement part of your AR application in native code, then you will need to ARToolKit native C/C++ dependencies.

##Prerequisites
Building native ARToolKit libraries requires a development environment capable of building native libraries for Android using the Android NDK. Currently, ARToolKit actively supports Android development systems of Mac OS X 9+ and Windows Desktop 8.1 and 10. However, there are those in the ARToolKit community who have successfully developed using Linux.

*Note: This is by no means a comprehensive guide on how to setup an NDK development environment. If you need assistance in this area, please search online as there are many tutorials and articles covering this topic and it is outside the scope of this user guide.*

#####Deprecated development tools and methods
> [Eclipse IDE][4]

> [ADT Plugin for Eclipse][5]

> Android NDK plugin for Eclipse

> Cygwin - previously required for Android development on Windows Desktop, replaced by Git bash

The following SDKs and tools should be installed and configured correctly on one of the chosen supported development systems.

#####These are required for standard Android JDK development:

- [Standard Edition Java Development Kit][1] 1.7 or greater
- [Android SDK][2] 
<p style="margin-left: 2em;">Downloaded with Android Studio IDE to</p>
<p style="margin-left: 4em;">for Mac OS X:</p>
<p style="margin-left: 6em;">default install path: *"/Users/&lt;user&gt;/Library/Android/sdk"*</p>
<p style="margin-left: 4em;">for Windows Desktop:</p>
<p style="margin-left: 6em;">recommended install path: *"C:\Users\\&lt;user&gt;\\Android\\sdk"*</p>
- [Android Studio IDE][3] - version 1.5.x

#####Requirements for building native code with the NDK within or outside of the Android Studio IDE:

- [Android NDK Preview][6] - The NDK that works with the Android Studio IDE.  Use the Android Studio IDE to download the NDK preview.
- [Git distributed version control system and Git bash][7] - requirement for both Windows Desktop and Mac OS X, Git Bash is not applicable to Mac OS X

---

####Regarding the Windows Desktop development environment

A few Unix commands are required for the Android NDK build script, `ndk-build.cmd`, to work. These commands are provided by the Git bash shell that comes with the Git download. Because of that, we can thankfully replace Cygwin - the Unix-like environment for Windows. Cygwin is seemingly an overkill for the meager requirements of `ndk-build.cmd` in that Cygwin large, invasive and the installation setup is confusing.

#####Special Git installation instructions for Windows Desktop only

When installing Git, from the Git setup wizard:

- Accept the default selected components
- For the "Adjusting your PATH environment" step, select the default "Use Git only"
- For the "Configuring the line ending conversions" step, select the default "Checkout Windows-style, commit Unix-style line ends"

---

Please try to ensure you have a working Android SDK and NDK environment before continuing. This, unfortunately, is not as easy as it sounds due the constantly evolving Android Studio tool set. Try the Hello-JNI steps described at [codelabs.developers.google][9].

For help with the Eclipse to Android Studio IDE transition, see the document https://github.com/artoolkit/artoolkit5/blob/master/AndroidStudioProjects/Docs/AS_Migration.pdf.

##Building Native Android Libraries
To build using the Android NDK toolchain, placed in the downloaded NDK is a script file, for Mac OS X, named `ndk-build` or, for Windows Desktop, named `ndk-build.cmd.` When Android Studio is used to download and install the NDK, by default, the NDK is installed directly under the Android SDK root folder. Also, by default, the NDK root folder is named "ndk-bundle." Therefore, the first step after installing the Android SDK and NDK is to set some environment variables (recommended for both Mac OS X and Windows Desktop development environments). For Windows Desktop, the following can be defined as Windows system environment variables or exported by the Git bash shell's ".bash_profile" startup file.

* Set ANDROID_HOME to indicate the path to root folder of the downloaded Android SDK.
* Set NDK to indicate the path to root folder (most likely, "ndk-bundle") of the downloaded NDK. The ANDROID_HOME environment variable can be used to help define NDK.
* Set PATH to include a path to the `ndk-build[.cmd]` script file, that is, the path to the root folder of the NDK. The NDK environment variable can be used to help define the added path.

Then, for both Mac OS X and Windows Desktop, re-source the command-line shell so that updated environment variables are seen by subsequent command-line shells. 

Next, proceed to the "android" folder directly off the root folder of the ARToolKit SDK or local repository. There are two script files that are used on both the Mac OS X and Windows Desktop development environments:

* build.sh - builds ARToolKit Android native C/C++ binaries for several Android Application Binary Interfaces ([ABIs][10])
* build_native_examples.sh - builds those ARToolKit Android Studio example app projects that contain both native C/C++ and Java source code, again, for several Android ABIs

Both scripts utilize the Android NDK and toolchain through the `ndk-build` script.

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

Once the native dependencies are built and copied, open an Android Studio example project and build the project's Java source files. If all builds, deploy to an Android simulated device or a *real* development device. Note: the camera doesn't work on simulated devices so it's best to test with *real* devices.

To use the native ARToolKit binaries in your own Android application, you will need to copy the *libs* folder generated by the "build.sh" script to your Android application project folder using the following project offset:

<p style="margin-left: 2em;">
 &lt;Android Studio Project&gt;/&lt;module&gt;/src/main
</p>

---

####Note

The provided ARToolKit Android Studio projects do not yet fully drive the native C/C++ build process from within the Android Studio IDE. This is partly because NDK development support is not seamlessly integrated into Android Studio as of yet. Rest assured it's the ARToolKit team's goal to achieve full native build integration with Android Studio going forward.

---

[1]: http://www.oracle.com/technetwork/java/javase/downloads/index.html
[2]: http://developer.android.com/sdk/index.html
[3]: http://developer.android.com/sdk/index.html
[4]: http://www.eclipse.org/
[5]: http://developer.android.com/sdk/eclipse-adt.html
[6]: http://tools.android.com/tech-docs/android-ndk-preview
[7]: https://git-scm.com
[9]: https://codelabs.developers.google.com/codelabs/android-studio-jni/index.html?index=..%2F..%2Findex#0
[10]: http://developer.android.com/ndk/guides/abis.html

[android_developing]: 4_Android:android_developing