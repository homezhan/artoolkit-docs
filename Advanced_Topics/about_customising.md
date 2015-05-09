# Customising Other Aspects of ARToolkit

##Changing Marker Border Width
The border width can be set at run time. See the documentation for [arSetPattRatio][1]

##Changing Marker Template Size
The maker template size (the number of pixels sampled in the marker image) IS editable, in `include/AR/config.h` (or config.h.in if you want to make the change permanent). The values in question are `AR_PATT_SIZE_X` and `AR_PATT_SIZE_Y` and `AR_PATT_SAMPLE_NUM` *which must be an integer multiple of the pattern size*.

## Using Really Large Images
If using large images, you may want to edit `#define`s `AR_SQUARE_MAX`, `AR_CHAIN_MAX`, and `AR_PATT_NUM_MAX` in config.h. These influence memory use so are usually set to a conservative minimum.

[1]: http://www.artoolworks.com/support/doc/artoolkit4/apiref/ar_h/index.html#//apple_ref/c/func/arSetPattRatio