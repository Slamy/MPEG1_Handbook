# Pink

Documentation about this tool is lacking. It is used to multiplex MPEG video and audio streams together for playback by a Philips CD-i.

## Prerequisites

You will find this program as part of a [cdi-sdk](https://github.com/TwBurn/cdi-sdk/tree/master).
`pink.exe` is a 16 Bit MS-DOS application. You may require an emulator like DOSBox to execute.

## Usage

Create a file like `pink.psc` with this content

    CDI "VIDEO01.MMD" pattern 0xFFFF from
        audio    "audio.mp2"
        start    0
        stream   0

        video    "video.m1v"
        start    0
        stream   0

Now execute this on your MS-DOS environment

    pink pink.psc

It will create `VIDEO01.MMD` which can be integrated into a green book disc using this entry.

    green       file    videoRtf    from record real_time mpeg vid01 in channel 0 from "BUILD/VIDEO01.MMD" eors at vid01.last

TODO Add an example MPEG player
