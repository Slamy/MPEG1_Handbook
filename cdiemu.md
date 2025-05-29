# Testing on emulated Philips CD-i for compliance

Since not all Video-CD players are compatible with CD-RW, it would be helpful to check the authored image before wasting a CD-R.

[This CD-i emulator](https://www.cdiemu.org/) is known to emulate the Digital Video Cartridge to some extent. Use it to confirm that

* The CD-i bridge application is provided on disc
* The MPEG stream satisfies the movie player

## Prerequisites

To avoid copyright infringement, cdiemu doesn't distribute the ROMs required for MPEG decoding.
They can be extracted legally from a real CD-i via a link cable using [cdilink](https://www.cdiemu.org/?body=site/cdilink.htm).

Since this process can become quite elaborate, the easy way out is a search for `cdi490a.zip` in the context of the `MAME` emulator.
This archive contains `vmpega.rom` which needs to be placed into the `rom` folder of `cdiemu`

## Testing without much mouse control

To start an image without mouse usage:

    wine wcdiemu-v053b8.exe path_to_vcd.bin -playcdi -start

