# Customising Other Aspects of ARToolkit

## Changing the width of the marker border

Prior to ARToolKit Professional v4.5, the border width was not directly editable. You could use a narrower border on your marker image, but it didn't make the extra space gained part of the pattern template.

With ARToolKit Professional v4.5 and later, the border width can now be set at run time. See the documentation for [arSetPattRatio][1]

## Changing the size of the marker template

The maker template size (the number of pixels sampled in the marker image) IS editable, in include/AR/config.h (or config.h.in if you want to make the change permanent). The values in question are AR_PATT_SIZE_X and AR_PATT_SIZE_Y and AR_PATT_SAMPLE_NUM which must be an integer multiple of the pattern size.

## Using really large images

Large images: if you need to go larger than 1024 pixels in either the horizontal or vertical dimensions of your image, you'll need to adjust the buffer size in arLabeling.c. This limit is removed in ARToolKit Professional v4.3 and later.

Also, if using large images, you may want to edit \#define AR_SQUARE_MAX, AR_CHAIN_MAX, and AR_PATT_NUM_MAX in config.h. These influence memory use so are usually set to a conservative minimum.

[1]: http://www.artoolworks.com/support/doc/artoolkit4/apiref/ar_h/index.html#//apple_ref/c/func/arSetPattRatio