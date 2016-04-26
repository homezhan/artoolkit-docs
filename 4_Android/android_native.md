#Android Native Development
The ARToolKit SDK package and the git cloned GitHub local repository of "artoolkit5" includes prebuilt native libraries. It's advised that a local repository be used since the downloaded SDK package is rarely up-to-date with the repository. If you are not planning on altering any native code then you do not need to consult this section or install the Android NDK. On the other hand, if you want to implement part of your AR application in native code, then you will need to build ARToolKit native C/C++ dependencies.

##Prerequisites
Building native ARToolKit libraries requires a development environment capable of building native libraries for Android using the Android NDK (NDK 11+). Currently, ARToolKit actively supports the Android development systems of Mac OS X 9+ and Windows Desktop 8.1 and 10. However, there are those in the ARToolKit community who have successfully developed using Linux.

>Note: This is by no means a comprehensive guide on how to setup an NDK development environment. If you need assistance in this area, please search online as there are many tutorials and articles covering this topic and it is outside the scope of this user guide.

The following SDKs and tools should be installed and configured correctly on one of the chosen supported development systems.

#####These are required tools for standard Android SDK development:

- [Standard Edition Java Development Kit][1] 1.7 or greater
- [Android Studio IDE][3] - version 1.5.x or greater
- [Android SDK][2] (Downloaded with Android Studio IDE)     
  - On Mac OS X: Default install path: **/Users/[username]/Library/Android/sdk**
  - On Windows Desktop: Recommended install path: **C:\Users\[username]\Android\sdk**

- Android NDK: Download and installation details described below

#####Requirements for building native code with the NDK within or outside of the Android Studio IDE:

- [Android NDK Preview][6] - The NDK that works with the Android Studio IDE.  Use the Android Studio IDE to download and setup the NDK preview requirements.
- [Git distributed version control system and Git bash][7] - Git DVCS is a requirement for Windows Desktop and Mac OS X. Git bash is a requirement for Windows Desktop and is not applicable to Mac OS X.

######Deprecated development tools and methods:

- Eclipse IDE
- ADT Plugin for Eclipse
- Android NDK plugin for Eclipse
- Cygwin

---

####Regarding the Windows Desktop development environment

A few Unix commands are required for the Android NDK build script, `ndk-build.cmd`, to work. These commands are provided by the Git bash shell that comes with the Git download. Because of that, we can thankfully replace Cygwin, the Unix-like environment for Windows, with Git bash. Cygwin is seemingly impractical for the meager requirements of `ndk-build.cmd` in that the Cygwin installation is large, invasive and the installation setup is confusing.

#####Special Git installation instructions for Windows Desktop only

When installing Git, from the Git setup wizard:

- Accept the default selected components
- For the "Adjusting your PATH environment" step, select the default "Use Git only"
- For the "Configuring the line ending conversions" step, select the default "Checkout Windows-style, commit Unix-style line ends"

---

Please try to ensure you have a working Android SDK and NDK environment before continuing. This, unfortunately, is not as easy as it sounds due the constantly evolving Android Studio tool set. Try the Hello-JNI tutorial available from [codelabs.developers.google.com][9]. Try implementing Hello-JNI app using NDK version 11+ for reasons explained below. Strive to use the latest and greatest developers.android.com supported Gradle plugin (com.android.tools.build:gradle-experimental:x.x.x) and Gradle version (http://services.gradle.org/distributions/gradle-x.x-all.zip) combination. Depending on the supported combination of experimental Gradle plugin and Gradle version used, there are differing required source updates to the HelloAndroidJni modules' build.gradle file.

In the tutorial, the step #5 of the "Add JNI Code Into Project" chapter, the C/C++ jni function prototype and the "jni" directory may not be created by the IDE as the IDE is supposed to do. If the IDE fails to create both, it's important to manually create the directory, `jni`, here: `[module root]/src/main/`. Once the jni directory is created you may try again to let the IDE create the `hellp-android-jni.c` file. If that fails, create and place the prototype C source file, `hello-android-jni.c`, in the `jni` directory. Add the required C source code as presented by step #5 of the tutorial.

Finally, once you create the new Hello-JNI Android Studio project and module, reduce the complexity of the module by deleting the "Test" directory from within the the IDE found under `[module root: "app"]/src/` in the Project pane.

Keep in mind that the tutorial is written for Android Studio executed on Linux or Mac OS X but Android Studio executed on Windows 10 will work as well.

> Minor Android Studio for Windows Difference: Step #7 of the "Create Java Sample App" chapter, in Android Studio: open "File" menu item, click to select "Settings...", open "Build, Execution, Deployment" twirl, open "Build Tools" twirl, open "Gradle" twirl, under "Project-level settings" group-box, ensure that "Use default gradle wrapper (recommended)" is selected.

For help with the Eclipse to Android Studio IDE transition, see the document [[https://github.com/artoolkit/artoolkit5/blob/master/AndroidStudioProjects/Docs/AS_Migration.pdf]].

##Building Native Android Libraries
To build using the Android NDK toolchain, placed in the downloaded NDK is a script file, for Mac OS X, named `ndk-build` or, for Windows Desktop, named `ndk-build.cmd.` When Android Studio is used to download and install the NDK, by default, the NDK is installed directly under the Android SDK root folder. Also, by default, the NDK root folder is named "ndk-bundle."

> Note: Due to the knife-edge roll of NDK version 11 by developers.android.com, it's recommended that ARToolKit Android developers download, install and use NDK version 11 or greater. Not doing so can result in link incompatibilities between your native libraries and their dependency on ARToolKit prebuilt native libraries. 

The next step after installing the Android SDK and NDK is to set some environment variables (recommended for both Mac OS X and Windows Desktop development environments). For Windows Desktop, the following can be defined as Windows system environment variables or exported by the Git bash shell's `.bash_profile` startup file.

* Set ANDROID\_HOME to indicate the path to root folder of the downloaded Android SDK.
* Set ANDROID\_NDK\_ROOT to indicate the path to root folder (most likely, "ndk-bundle") of the downloaded NDK. The ANDROID\_HOME environment variable can be used to help define NDK. `ANDROID_NDK_ROOT=$ANDROID_HOME/ndk-bundle`
* Set NDK to the same path as ANDROID\_NDK\_ROOT. `NDK=$ANDROID_NDK_ROOT`
* Set PATH to include a path to the `ndk-build[.cmd]` script file, that is, the path to the root folder of the NDK. The NDK environment variable can be used to help define the added path.

Then, for both Mac OS X and Windows Desktop, re-source the command-line shell so that updated environment variables are seen by subsequent command-line shells. 

Next, proceed to the "android" folder directly off the root folder of the ARToolKit SDK or local repository. There are two script files that are used on both the Mac OS X and Windows Desktop development environments:

* build.sh - builds ARToolKit Android native C/C++ binaries for several Android Application Binary Interfaces ([ABIs][10])
* build\_native\_examples.sh - builds those ARToolKit Android Studio example app projects that contain both native C/C++ and Java source code, again, for several Android ABIs

Both scripts utilize the Android NDK and toolchain through the `ndk-build` script.

To build, from the bash command-line (for Windows Desktop, this will be the Git bash shell), execute the `./build.sh` script file, without arguments. When `build.sh` completes without errors, there will be dependencies built for several Android ABIs here: 

* Mac OS X: `/[ARTK SDK or repo root]/android/libs`
* Windows Desktop: `C:\[ARTK SDK or repo root]\android\libs`

These are the ARToolKit binaries built for the various Android ABIs. The Android Studio example projects, that don't include native C/C++ source code, are populated with the content of the generated *libs* folder.

To build the Android Studio example app projects that do include native C/C++ source code and to build the project's C/C++ source, after executing the `./build` script file, execute `./build_native_examples.sh`, without arguments. When `build_native_examples.sh` script completes without errors, the native Android Studio example projects are populated with the content of the generated *libs* folder. Using an actual example Android Studio project, "ARSimpleNativeProj," the *libs* folder is copied here:

```
[ARTK SDK or repo root]/AndroidStudioProjects/ARSimpleNativeProj/aRSimpleNative/src/main/
```

Once the native dependencies are built and copied, open an Android Studio example project and build the project's Java source files. If all builds, deploy to an Android simulated device or a *real* development device. Note: the camera doesn't work on simulated devices so it's best to test with *real* devices.

To use the native ARToolKit binaries in your own Android application, you will need to copy the *libs* folder generated by the "build.sh" script to your Android application project folder using the following project offset:

```
[Android Studio Project root]/[module root]/src/main
```

---

####Note

The provided ARToolKit Android Studio projects do not yet fully drive the native C/C++ build process from within the Android Studio IDE. This is partly because NDK development support is not seamlessly integrated into Android Studio as of yet. Rest assured it's the ARToolKit team's goal to achieve full native build integration with Android Studio going forward.

---

[1]: http://www.oracle.com/technetwork/java/javase/downloads/index.html
[2]: http://developer.android.com/sdk/index.html
[3]: http://developer.android.com/sdk/index.html
[4-not used]: http://www.eclipse.org/
[5-not used]: http://developer.android.com/sdk/eclipse-adt.html
[6]: http://tools.android.com/tech-docs/android-ndk-preview
[7]: https://git-scm.com
[9]: https://codelabs.developers.google.com/codelabs/android-studio-jni/index.html?index=..%2F..%2Findex#0
[10]: http://developer.android.com/ndk/guides/abis.html

[android_developing]: 4_Android:android_developing