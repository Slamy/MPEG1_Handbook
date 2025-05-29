# MPEG1 Handbook

This project aims to be a collection of knowledge about MPEG1 encoding and Video-CD authoring.

MPEG1 is a lossy video compression codec which happens to be used with the Video-CD and the Philips CD-i.
Since the creation of MPEG2 and its usage with the DVD, MPEG1 became commercially obsolete.
Due to this loss of relevance, the knowledge about high quality MPEG1 encoding was scattered and popular
encoding tools like `FFmpeg` don't provide acceptable results.

## Target audience

* You want to master/author a Video-CD
* You want to create full motion video for the Philips CD-i

The tutorials are written with Linux in mind. Nevertheless, most of the info is applicable on other systems as well.

## Prerequisites for the examples

This handbook provides examples to encode the free short movie [Big Buck Bunny](https://peach.blender.org/).
Please click [here](https://download.blender.org/peach/bigbuckbunny_movies/big_buck_bunny_1080p_h264.mov) to
download a 1080p H264 version of it for testing.

You can also use `wget` on the terminal for download:

    wget https://download.blender.org/peach/bigbuckbunny_movies/big_buck_bunny_1080p_h264.mov

## Content

* [Encoding using FFmpeg](ffmpeg.md)
* [Encoding using TMPGEnc](tmpgenc.md)
* [Authoring Video-CDs](vcd.md)
* [Authoring Green Book MPEG streams using the pink tool](pink.md)
* [Testing on emulated Philips CD-i to check compatibility](cdiemu.md)
* [Troubleshooting common issues](troubleshooting.md)
* [Encoding using mencoder](mencoder.md)

## Limitations of the Video-CD

* Video
  * MPEG-1
  * Progressive scan (no interlacing! MPEG-2 was designed to fix this)
  * bitrate fixed at 1150 kb/s
  * resolution is 352 x 288 @ 25 fps for PAL
  * resolution is 352 x 240 @ 29.97 fps for NTSC
* Audio
  * MPEG-1 Layer II (MP2)
  * bitrate fixed at 224 kb/s

## Terminology

* MPEG elementary streams contain only video or audio. Typical endings are `.m1v` for video and `.mp2` for audio.
* `pink` is a MS-DOS tool to store MPEG audio and video elementary streams as green book compatible records

## References

* [FFMPEG Video Options](https://ffmpeg.org/ffmpeg.html#Video-Options)
* [Encoding MPEG with Mencoder](http://www.mplayerhq.hu/DOCS/HTML/de/menc-feat-mpeg.html)
* [Encoding VCD with Mencoder](http://www.mplayerhq.hu/DOCS/HTML/de/menc-feat-vcd-dvd.html)
* [Mentions of FFmpeg failing with I-Frame quality in 2014](https://stackoverflow.com/questions/26802420/how-to-avoid-pumping-artifacts-when-encoding-still-images-into-a-mpeg-2-video-us/26807279)
* [Mentions of FFmpeg failing with I-Frame quality in 2007](https://ffmpeg-user.ffmpeg.narkive.com/kz70RuoG/mpeg-1-video-quality-vs-tmpgenc)
* [Big Buck Bunny](https://peach.blender.org/)
* [Big Buck Bunny Downloads](https://download.blender.org/peach/bigbuckbunny_movies/)
