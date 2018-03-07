## Updates

Firmware updates itself upon every device boot if necessary. Please do not interrupt the update process, even if the "UPDATING" sign will stop rotating.

## Factory reset

Please press the button for about 10 seconds. All settings including wi-fi passwords will be erased and new device's UUID will be generated.

## Firmware re-flash

If you need to reflash firmware in your device, use following sketch:

<script src="https://gist.github.com/kubicek/da4f12b3c6e649a6ec57292610721fc4.js"></script>

Or do it manualy:

    $ curl https://update.cryptoclock.net/esp/update?model=3DA0100 >> 3DA0100.bin
    $ esptool -vv -cd nodemcu -cb 115200 -cp /dev/cu.wchusbserial1420 \\
        -ca 0x00000 -cf 3DA0100.bin
