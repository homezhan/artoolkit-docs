# Running the SimpleNFT Example

## Quick start

Open a command-line window (Terminal on Mac OS X/Linux, cmd.exe on Windows). Navigate to your ARToolKitNFT/bin directory. The NFT data set to use must be specified as a command-line argument. As a sample, one page of the Magicland is provided in ARToolKitNFT/bin/Data/MagicLand3/. This directory also contains the required feature maps, sets, etc.

## Launching simpleNFT

We will use the sample “MagicLand” story by Hirokazu Kato to demonstrate the NFT tracking, via the sample code simpleNFT.

1. Print out the jpeg file bin/Data/MagicLand3/MagicLand.jpg on a colour printer.

> The image is 1568 pixels wide and 2164 pixels high, with a resolution of 200 dots per inch (dpi). When printed at 1:1 scaling, its printed size should be 199.1 mm wide and 274.8 mm tall. This should just fit onto a sheet of A4 paper (210 mm x 297 mm) on most printers.
> If instead you wish to print the image on US Letter paper (8.5 inches x 11 inches) the image will need to either be cropped top and bottom, or scaled to fit. Cropping will maintain correct distance measurements in ARToolKit NFT, at the cost of perhaps losing some of the tracking points, whereas scaling will result in measurements returned by ARToolKit being scaled by the same amount.

The simpleNFT example expects its configuration file to be specified as a command-line argument. This means it needs to be either run from a command or terminal window, or from a shell which can pass command-line arguments.

2. On Windows, open a command-shell by typing “cmd” in the “Run” box found on the Windows start menu. On Mac OS X or Linux, open a Terminal window.

3. Change the working directory in your command shell to the ARToolKitNFT bin directory. On Windows and Mac OS X, you can type “cd” then leave a space, then drag the bin folder onto the command window; the full path to the bin folder should be entered automatically.

4. Type the command to launch simpleNFT, providing the path to the config file.

> For our example, one sample page of the Magicland story is provided in ARToolKitNFT/bin/Data/MagicLand3/. This directory also contains the required feature maps, sets, ...
> To use the sample, type `simpleNFT.exe Data/MagicLand3/config.dat` on Windows, or `./simpleNFT Data/MagicLand3/config.dat` on Mac OS X or Linux.

5. Once the application is running, point the camera at the image. Start by pointing it at the black square labelled “Map” to initialise the tracking. Once the marker is recognised, yellow squares will be drawn on top of the page. Then, if pre-trained features on the page are recognised by the NFT tracker, the yellow squares will turn red.

A green border will also be drawn around the outline of the page.

## Changing settings while running simpleNFT

The simpleNFT also allows parameters of the tracking to be changed, and some debug information to be displayed by pressing keys. The following keys are active:

<table rules="all" style="margin:1em 1em 1em 0; border:solid 1px #AAAAAA; border-collapse:collapse;empty-cells:show;" border="2" cellpadding="3" cellspacing="4">

<tbody><tr>
<th> Key </th><th> Function
</th></tr>
<tr>
<td>esc </td><td> Quit the application.
</td></tr>
<tr>
<td>1</td><td> Toggle tracking mode between interlaced mode (FIELD_IMAGE, used for DV cameras) and non-interlaced mode (FRAME_IMAGE, used for normal cameras).
</td></tr>
<tr>
<td>2</td><td> Toggle tracking mode between normal and fine NFT tracking.
</td></tr>
<tr>
<td>3</td><td> Reduce similarity threshhold, i.e. be more permissive in matches between features in incoming video and surface.
</td></tr>
<tr>
<td>4</td><td> Increase similarity threshhold, i.e. be more strict in matches between features in incoming video and surface.
</td></tr>
<tr>
<td>b</td><td> Toggle between constant and adaptive blurring of tracked image.
</td></tr>
<tr>
<td>7</td><td> Reduce blur level.
</td></tr>
<tr>
<td>8</td><td> Increase blur level.
</td></tr>
<tr>
<td>(space)</td><td> Toggle capture mode, in which video frames are recorded for later playback.
</td></tr>
<tr>
<td>r</td><td> Toggle between realtime tracking and tracking from recorded frames.
</td></tr>
<tr>
<td>9</td><td> If tracking from recorded frames, switch to an earlier recorded frame than the current frame.
</td></tr>
<tr>
<td>0</td><td> If tracking from recorded frames, switch to a later recorded frame than the current frame.
</td></tr>
<tr>
<td>d:</td><td>Turn on black-and-white debug mode.. you will see the binarised image as ARToolKit sees it. Recognised markers will be drawn with a red outline.
</td></tr>
<tr>
<td> –</td><td> Reduce the binarisation threshold by 5 units (range 0 – 255).
</td></tr>
<tr>
<td> +</td><td> Increase the binarisation threshold by 5 units (range 0 – 255).
</td></tr>
<tr>
<td>f</td><td> Turn on NFT debug mode. Information about the resolution of the tracked image in x and y dimensions of the page will be displayed to the console. Press again to see candidate features as they are extracted from the image.
</td></tr>
<tr>
<td>[ </td><td><b>Linux lib1394 video input only</b> Decrease camera shutter speed.
</td></tr>
<tr>
<td>] </td><td><b>Linux lib1394 video input only</b> Increase camera shutter speed.
</td></tr></tbody></table>