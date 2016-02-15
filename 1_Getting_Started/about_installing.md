# Installing ARToolKit
The ARToolKit distribution is supplied as pre-built binaries for each platform, plus source code for most of the SDK libraries and utilities, full source for the examples, and documentation.

You, of course, are always welcome to [clone the source code][repo] and [build it yourself][building], as well.

## Windows
Run the ARToolKit installer executable and follow the prompts.

By default, ARToolKit will be installed into a folder inside your Program Files folder. Start menu items are created to allow you to quickly open the folder containing the installed software, to open a command-line prompt with the path set to this folder, and to read documentation and access this support site. The installer also automatically creates the ARTOOLKIT5_ROOT environment variable to point to your chosen install location.

If you are upgrading to a newer version, it is generally safe to install over the old version. Before upgrading, save any modifications you have made to any ARToolKit source or example code, and then run the installer. The installer will add or update new files, and remove unneeded old files.

## Mac OS X / Linux
The SDK is supplied as an archive file (.tar.gz or .zip file) which need only be unpacked to a location of your choice (we recommend `~/SDKs/`). Drop the archive into your chosen location. In OS X, all you have to do is double-click the archive to unpackage it. In Linux, use the following command in your terminal:
<pre>
    tar xzvf ARToolKit5-bin-*.tar.gz
</pre>

Once unpacked, to set the [ARTOOLKIT5_ROOT so that other software can find ARToolKit][setting_env], open a Terminal window, and run the script artoolkit5-setenv:
<pre>
    // Example assumes ARToolKit is in ~/SDKs/
    cd ~/SDKs/ARToolKit5/
    ./share/artoolkit5-setenv
</pre>

## Verifying the Installation
ARToolKit includes a variety of examples demonstrating ARToolKit programming techniques. After installation, the executables for these applications can be found in the `bin` directory inside your ARToolKit directory. Running the simpleLight example is one of the most straight-forward ways to test that your ARToolKit installation is functioning correctly. An explanation of simpleLight, including how to run it, and its sourcecode can be found on the page [ARToolKit Tutorial 1: First Simple ARToolKit Scene][tutorial_1_first_scene].

## Beginning your own development
When beginning your own development, it is recommended that you create your own project outside the ARToolKit folder, and treat ARToolKit as an external SDK. However, it is also perfectly permissible to begin by modifying one or more of the example applications or source files. ARToolKit is supplied with project files for each supported platform. The project files allow you to [rebuild ARToolKit from source][building], and act as examples of how to structure your own application builds (e.g. required link libraries).

[repo]: https://github.com/artoolkit
[building]: 8_Advanced_Topics:build_artoolkit
[setting_env]: 1_Getting_Started:general_environment_variables
[tutorial_1_first_scene]: 7_Examples:example_simplelite
[3]: http://developer.apple.com/xcode/
[4]: http://www.apple.com/quicktime/download/
[5]: http://www.artoolworks.com/dist/openscenegraph/
[6]: http://mesa3d.sourceforge.net/
[7]: http://www.openvrml.org/
