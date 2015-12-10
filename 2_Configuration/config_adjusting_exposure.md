#Adjusting for Over-/Under-Exposed Video Sources
Part of ARToolKit's tracking operates on a binarized image, that is, an image that has been converted into black and white pixels only. All pixels above a certain level of brightness, referred to as the "binarization threshold", or just "threshold" are converted to white, and all pixels below this threshold are converted to black.

The binarization threshold is an 8-bit number that is in the range `[0, 255]`, inclusive. The default value is usually set in the middle of this range, allowing ARToolKit to easily find markers in images that have good contrast. The default value is defined by the symbol `AR_DEFAULT_LABELING_THRESH` in arConfig.h.

Where images have poor contrast, or are over- or under-exposed, the default binarization threshold should be adjusted to compensate. This is achieved by calling the ARToolKit function `arGetLabelingThresh()` to get the current threshold value, adjusting it up for an image that is too bright, or down for an image that is too dark, and then calling `arSetThreshold()` with the new value. This is demonstrated in this snippet from the simpleLite example:
<pre>
    static void Keyboard(unsigned char key, int x, int y)
    {
        int threshChange = 0;
        switch (key) {
            case '-':
                threshChange = -5;
                break;
            case '+':
            case '=':
                threshChange = +5;
                break;
            default:
                break;
        }
        if (threshChange) {
            int threshold;
            arGetLabelingThresh(gARHandle, &threshold);
            threshold += threshChange;
            if (threshold < 0) threshold = 0;
            if (threshold > 255) threshold = 255;
            arSetLabelingThresh(gARHandle, threshold);
            printf("threshold changed to %d.\n", threshold);
        }
    }
</pre>

How does the user know how much adjustment to make? The simplest way is to let the user see the image as ARToolKit sees it. ARToolKit includes a "debug" mode to facilitate this.

The debug mode can be toggled on and off easily, as seen in this snippet from the simpleLite example:
<pre>
static void Keyboard(unsigned char key, int x, int y) 
{
    int mode;
    switch (key) {
        case 'D':
        case 'd':
            arGetDebugMode(gARHandle, &mode);
            arSetDebugMode(gARHandle, !mode);
            break;
        default:
            break;
    }
}
</pre>

For examples based on use of the gsub_lite library (as simpleLite is), the debug image will be drawn in place of the regular image by the call to `arglDispImage()` whenever debug mode is enabled.

For examples based on the gsub library (e.g. simpleTest), the debug image must be manually drawn.