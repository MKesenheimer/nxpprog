# Programmer for NXP arm processors using ISP protocol.

For help run the command with no arguments:

```
./nxpprog.py
```

Program image file to processor:

```
./nxpprog.py <serial device> <image_file>
```

The image start address defaults to 0.
When the image start address is 0 a checksum is inserted in the reserved
interrupt vector so that the bootloader will boot the image.
The image file is a raw binary file (output from objcopy -O binary).

Note:
Xonxoff flow control does not work with some usb serial
converters on windows and doesn't seem necessary in my setup.
If you in your setup need flow control, for example
if you get programming errors, then try enabling this.

## Windows Advice

When you have installed python for windows and the (py)serial module
then something like this should work:

```
<path to python>\python.exe nxpprog.py COM1 image.bin
```

It is very important that the serial port name is written in capital letters,
lower case names will not be matched against possible serial devices.

## Examples programming the LPC1311

Flash an image:

```
python nxpprog.py --eraseall /dev/tty.usbserial-A50285BI test.bin
```

Check if flash is blank after programming (should fail):

```
python nxpprog.py --blankcheck /dev/tty.usbserial-A50285BI
```

Dump image:

```
python nxpprog.py --read dump.bin --addr=0 --len=32 /dev/tty.usbserial-A50285BI
```