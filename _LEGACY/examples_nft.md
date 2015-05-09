# ARToolkit NFT Examples

ARToolKit NFT includes some examples demonstrating ARToolKit NFT programming techniques. The executables for these applications can be found in the "bin" directory inside your ARToolKit NFT installation, and the source code for the examples can be found in the "examples" directory.

## What do the examples do?

There are 5 example programs in ‘Example’ directory. The ‘exampleNFT0’ is the simplest one. The ‘exampleNFT4’ is the most complicated one.

- exampleNFT0: This program reads a single NFT and KPM dataset for a single textured marker surface and displays graphics on the surface. The processing flow is very simple.
- exampleNFT1: This is almost same as exampleNFT0 but has some optional features to see the effect of changing the various tracking parameters.
- exampleNFT2: This program reads multiple target files. It detects one of them and put the virtual object on it. While the KPM is working, the framerate is usually slow.
- exampleNFT3: This program also reads multiple target files, however it tries to detect all visible target textures (as opposed to a single target at a time) and it put virtual objects on all of them. Because KPM requires a lot of time, if you specify many targets, the framerate is always slow.
- exampleNFT4: The functionality of exampleNFT4 is almost same as exampleNFT3. However, this example uses threads to run the tracking process asynchronously. Therefore it allows framerate of the display to keep up with the higher framerate of the camera even if the KPM is very slow.
- exampleNFTWithFiducial: this program demonstrates a less resource-intensive technique using a combination of marker tracking and NFT 1.0 tracking. KPM and OpenCV libraries are therefore not required.

## How to launch the examples:

- For exampleNFT0/1/2/3, the NFT data set(s) to use must be specified as command-line argument(s). A single sample dataset is provided in the directory bin/Data/pinball/.

1.  Print the image bin/Data/pinball/pinball.jpg
2.  Open a command-line window (Terminal on Mac OS X/Linux, cmd.exe on Windows).
3.  Navigate to your ARToolKitNFT/bin directory.
4.  The invocation is slightly different depending on the platform:
<pre>
Windows: exampleNFT0.exe Data\pinball\pinball.dat
Mac OS X: ./exampleNFT0.app/Contents/MacOS/exampleNFT0 Data/pinball/pinball.dat
Linux: ./exampleNFT0 Data/pinball/pinball.dat
</pre>
- The exampleNFT4 program reads ‘Data/tracking.conf’ for setting up target data.
- The exampleNFTWithFiducial example takes the NFT data set to use from a command-line argument. A sample dataset is provided in the directory bin/Data/MagicLand3/.
1.  Print the image bin/Data/MagicLand3/MagicLand3.jpg
2.  Open a command-line window (Terminal on Mac OS X/Linux, cmd.exe on Windows).
3.  Navigate to your ARToolKitNFT/bin directory.
4.  The invocation is slightly different depending on the platform:
<pre>
Windows: simpleNFT.exe Data\MagicLand3\config.dat
Mac OS X: ./simpleNFT.app/Contents/MacOS/simpleNFT Data/MagicLand3/config.dat
Linux: ./simpleNFT Data/MagicLand3/config.dat
</pre>