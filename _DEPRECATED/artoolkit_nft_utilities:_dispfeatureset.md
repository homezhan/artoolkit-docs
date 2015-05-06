# ARToolkit NFT Utilities: dispFeatureSet

## Purpose

dispFeatureSet displays trained NFT datasets by overlaying representations of the data points on the source images.

## Usage

<pre>
./dispFeatureSet <filename>
 -fset     Show fset features.
 -fset2    Show fset2 features.
</pre>

After launching dispFeatureSet, the various image resolutions will be displayed on screen with the tracking features overlaid. The features used in continuous tracking are outlined by red boxes, and the features used in identifying the pages and initialising tracking are marked by green crosses.

![ARToolKit NFT - dispFeatureSet terminal][ARToolKit_NFT_-_dispFeatureSet_terminal]
![ARToolKit NFT - dispFeatureSet][ARToolKit_NFT_-_dispFeatureSet]

[ARToolKit_NFT_-_dispFeatureSet_terminal]: /ARToolKit_NFT_-_dispFeatureSet_terminal.png
[ARToolKit_NFT_-_dispFeatureSet]: /ARToolKit_NFT_-_dispFeatureSet.png