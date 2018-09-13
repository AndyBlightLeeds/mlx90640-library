# mlx90640-library
MLX90640 library functions

## Raspberry Pi Users

** EXPERIMENTAL **

This port uses either generic Linux I2C or the  bcm2835 library.

### Generic Linux I2C Mode

To get the best out of your sensor you should modify `/boot/config.txt` and change your I2C baudrate.

The fastest rate recommended for compatibility with other sensors is 400kHz. This is compatible with SMBus devices:

```text
dtparam=i2c1_baudrate=400000
```

This will give you a framerate of - at most - 8FPS.

If you're just using the MLX90640 and, for example, the 1.12" OLED, you can safely use 1MHz:

```text
dtparam=i2c1_baudrate=1000000
```

This will give you a framerate of - at most - 32FPS.

Now build the MLX90640 library and examples in LINUX I2C mode:

```text
make clean
make I2C_MODE=LINUX
```

### BCM2835 Library Mode

To use the bcm2835 library, install like so:


```text
make bcm2835
```

Or, step by step:

```text
wget http://www.airspayce.com/mikem/bcm2835/bcm2835-1.55.tar.gz
tar xvfz bcm2835-1.55.tar.gz
cd bcm2835-1.55
./configure
make
sudo make install
```

To install dependencies:

```text
sudo apt-get install libavutil-dev libavcodec-dev libavformat-dev
```

Then just `make` and `sudo ./test` or one of the other examples listed below:

# fbuf

```
sudo ./fbuf
```

This example uses direct-to-framebuffer rendering and black-blue-green-yellow-red-purple-white false colouring.

If you gave issues with the output image, set "`IMAGE_SCALE`" to a smaller number.

# interp

```
sudo ./interp
```

This example uses direct-to-framebuffer rendering and black-blue-green-yellow-red-purple-white false colouring.

It also has 2x bicubic resize filter.

If you have issues with the output image, set "`IMAGE_SCALE`" to a smaller number.

# test


```
sudo ./test
```

This example draws out to the console using ANSI colours and the full block char.

To see the actual temperature values, change "`FMT_STRING`" from the block char to the float format.

# step

```
sudo ./step
```

Attempt to run in step by step mode (experimental)

