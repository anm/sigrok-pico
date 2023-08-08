Building this should follow build flows similar to the documented build flows in libsigrok.
Note: These steps rely on a brute-force copy approach to move the 3 needed files under /libsigrok/src/hardware/raspberrypi-pico.  A cleaner way would be to pull a specific repo as the first step that has the sigrok-pico code in it, but this method helps ensure you can do a normal baseline build.  Once this gets officially released into sigrok mainline then the sigrokutil/ new driver steps can be skipped.

Do something like this:
1) git clone the mainline libsigrok, libsigrokdecode, sigrok-util, and pulseview.
2) Run sigrok-util to make a patch to apply to libsigrok.
   cd <path>/sigrok-util/source
   ./new-driver "RaspberryPI PICO"
   cd <path>/libsigrok
   git apply <path>/sigrok-util/source/0001-raspberrypi-pico-Initial-driver-skeleton.patch
6) copy api.c, protocol.c and protocol.h from https://github.com/sigrokproject/libsigrok/pull/181 into <path>/libsigrok/src/hardware/raspberrypi-pico
8) ./autogen.sh
9) ./configure
10) make install

Build the sigrokcli and/or pulseview per the documentation.
