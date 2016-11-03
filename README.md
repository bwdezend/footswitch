# footswitch
Code to drive a homegrown teensy based footswitch.  The footswitch is
operated by grounding PIN11 on the teensy (I currently use a reed switch
and a magnet), which sends a serial command to a python daemon which in
turn sets the macOS system input volume to 0. When the circuit opens,
the input volume is set to 100.

The config file sets the metrics reporting server, the serial port to
use and the prefix for the metrics reporting.

    [default]
    serialport = /dev/cu.usbmodemNNNNNN
    switchmetric = 1min.graphite.metric.prefix
    carbon_server = localhost
    carbon_port   = 2003

The mute-daemon python utility and the mute-atr.scpt must be executable
and in /usr/local/bin, and the config file should be in
/usr/local/etc/mute-daemon.cfg.


The teensy code should be loaded onto the board, and the mic is muted by
grounding PIN 11. If an LED is attached to PIN 9, it will illuminate
when the mic is "hot", and if an LED is attached to PIN 10, it will
illuminate when the mic is "cold". The LED will not change until the Mac
has muted the system-level input and the mute-daemon has responded to
the teensy.


Manually changing the mute state of the Mac will not be reflected by the
LED.