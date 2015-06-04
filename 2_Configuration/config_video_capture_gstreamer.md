# Configuring GStreamer Video Capture in ARToolKit

A variety of GStreamer pipelines can be constructed, for example to pull video from a webcam, local file, or network stream. These are the important points to observe regarding where ARToolKit fits into a GStreamer pipeline:

- ARToolKit accepts video only in 24-bit RGB format, so must be prefixed with a capsfilter element 'video/x-raw-rgb,bpp=24'. Usually, you will also need to use a 'ffmpegcolorspace' element to convert incoming video into this format, unless the upstream source can already produce this format.
- ARToolKit acquires the video from a GStreamer 'identity' element, with the property 'name=artoolkit'. You should also set the property 'sync=true' on this element, or else some types of sources (e.g. video from a file) may run faster or slower than normal.
- ARToolKit is NOT a sink pad, so generally, you should pipe the stream for ARToolKit to a 'fakesink' element.

Putting these points together, the last part of the GStreamer pipeline for ARToolKit will usually be:

`deo/x-raw-rgb,bpp=24 ! identity name=artoolkit sync=true ! fakesink`

Note also that ARToolKit will respect the size of incoming video, so you can add the 'width=' and 'height=' properties to the capsfilter element, should you so desire.

Some more examples:

- A webcam on /dev/video0 through Video4Linux v2 (V4L2): o0 use-fixed-fps=false ! ffmpegcolorspace ! video/x-raw-rgb,bpp=24 ! identity name=artoolkit sync=true ! fakesink
- A file from disk: er_test_xvid.avi ! decodebin2 ! ffmpegcolorspace ! video/x-raw-rgb,bpp=24 ! identity name=artoolkit sync=true ! fakesink
- A dummy test source: aw-rgb,bpp=24 ! identity name=artoolkit sync=true ! fakesink

Further interesting reading concerning GStreamer and webcam control:

- http://www.oz9aec.net/index.php/gstreamer/345-a-weekend-with-gstreamer
- http://www.oz9aec.net/index.php/gstreamer/367-webcam-pixel-formats-and-gstreamer-caps-filters.
- http://benlau.blog.opensource.hk/2008/09/gstreamer-pipeline-description.html
