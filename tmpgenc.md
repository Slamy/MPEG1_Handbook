# TMPGEnc

TMPGEnc is a professional MPEG encoding and multiplexing suite.
This manual is written for `TMPGEnc-2.525.64.184` which happens to be the last free version of this application.
For MPEG-1 this free version is sufficient. Since this is a Windows application, it is necessary to use Wine for execution on Linux.

## Prerequisites for running TMPGEnc on Wine

This software requires additional DLLs for decoding video. These are usually distributed with Microsoft Windows
but are either lacking or seemingly broken on Wine.
While multiplexing MPEG can be done without these, encoding requires decoding beforehand.

The tool `winetricks` offers installation of the required libraries with a single command.
Keep in mind that this only works for a 32 bit prefix.
First, we prepare a prefix with the required DLLs. It will download some setup files as well and require some
interaction with the installation wizards.

    WINEPREFIX="$HOME/prefix_tmpgec" WINEARCH=win32 winetricks allcodecs

Then use this to run TMPGEnc with the now created prefix

    WINEPREFIX="$HOME/prefix_tmpgec" WINEARCH=win32 wine TMPGEnc.exe

## Re-encoding MPEG Video elementary stream for `pink`

This assumes that you have created a high quality stream with `FFmpeg` or other tools before and want
to have it encoded at a quality better than `FFmpeg` can do for example.

* Browse for your Video Source
* Select Stream type `ES [Video only]`

The result will be a `*.m1v` file you can use with `pink`

## Re-encoding MPEG Video for VCDs

This assumes that you have created a high quality stream with `FFmpeg` or other tools before and want to
have it encoded at a quality better than `FFmpeg` can do for example.

It might be tempting to encode and mux at the same time. The stream type `System (Video + Audio)`
seems to be made exactly for that. For some reason, the result is not compatible with the Philips CD-i.
It probably is not enforcing the required muxing rate.

* Browse for your Video Source
* Select stream type `ES [Video only]`

The result will be a `.m1v` file. Use either `mplex` or the remuxing described below to create the full stream.

## Remuxing MPEG for VCD to fix an already existing file

Since `FFmpeg` has issues with muxing for VCD, we can use TMPGEnc to fix a stream by remuxing.

* File -> MPEG Tools...
* Simple Multiplex
* Ensure Type is set to `MPEG-1 Video-CD`
* Select both input streams for video and audio
* Run

The result is now compatible with the CD-i.
