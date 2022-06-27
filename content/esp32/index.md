
[Index](../../index.md)

---

# Programming Microcontrollers

> *Arduino IDE? Nah.*

I have an M5StickC. I want to program it in rust, but I need to crawl before I can walk.

## What is the M5stickC

It's a little orange box, with some hardware inside. Most notably,
an esp32-pico-d4. It has UART (Universal Asynchronous Receiver Transmitter) io, connected
to a UART to USB bridge. When plugged into my laptop, it shows up as `/dev/ttyUSB0`.

On arch linux, my user needed to be added to the uucp group - this gives read/write access to the serial device.

```
usermod -a -G uucp ethan
```

The CPU runs code. Call it firmware, call it whatever, it's just binary data in the cpu's memory.

If the code I write wants to do anything, it has to take libraries with it. The libraries abstract away the hardware interfaces, making them easier to work with.

ESPRESSIF, the company that makes the esp32, makes a collection of libraries and tools called the esp-idf. This
is a pretty good, minimal starting point.

Start here [https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/index.html#step-8-build-the-project](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/index.html#step-8-build-the-project)

I followed through to flashing the hello_world example program.

When flashing code to the device, the default baud rate doesn't work! Use:

```
idf.py -p /dev/ttyUSB0 -b 115200 flash
```

Now, what's going on?

- There's code on there
- The system is running it
- It's writing data to serial with printf

How do we read it?

Let's take a look at the serial device:

```sh
# Get info
stty -F /dev/ttyUSB0
```

The baud rate is what we set when we uploaded the code, and other than that, it figured itself out.

To recieve data from the serial interface, use screen:

```sh
# screen <device> <baud>
screen /dev/ttyUSB0 115200
```

End your screen session by entering screen's command mode with `Ctrl+A`, and then kill with `k`.

yoooooo it worked!

```
I (13) boot: ESP-IDF v4.3.2 2nd stage bootloader
I (13) boot: compile time 13:29:51
I (13) boot: chip revision: 1
I (14) boot_comm: chip revision: 1, min. bootloader chip revision: 0
I (21) boot.esp32: SPI Speed      : 40MHz
I (26) boot.esp32: SPI Mode       : DIO
I (31) boot.esp32: SPI Flash Size : 2MB
I (35) boot: Enabling RNG early entropy source...
I (41) boot: Partition Table:
I (44) boot: ## Label            Usage          Type ST Offset   Length
I (51) boot:  0 nvs              WiFi data        01 02 00009000 00006000
I (59) boot:  1 phy_init         RF data          01 01 0000f000 00001000
I (66) boot:  2 factory          factory app      00 00 00010000 00100000
I (74) boot: End of partition table
I (78) boot_comm: chip revision: 1, min. application chip revision: 0
I (85) esp_image: segment 0: paddr=00010020 vaddr=3f400020 size=06da0h ( 28064) map
I (104) esp_image: segment 1: paddr=00016dc8 vaddr=3ffb0000 size=02934h ( 10548) load
I (108) esp_image: segment 2: paddr=00019704 vaddr=40080000 size=06914h ( 26900) load
I (122) esp_image: segment 3: paddr=00020020 vaddr=400d0020 size=13a74h ( 80500) map
I (151) esp_image: segment 4: paddr=00033a9c vaddr=40086914 size=049b8h ( 18872) load
I (159) esp_image: segment 5: paddr=0003845c vaddr=50000000 size=00010h (    16) load
I (165) boot: Loaded app from partition at offset 0x10000
I (165) boot: Disabling RNG early entropy source...
I (180) cpu_start: Pro cpu up.
I (180) cpu_start: Starting app cpu, entry point is 0x40081044
I (174) cpu_start: App cpu up.
I (194) cpu_start: Pro cpu start user code
I (194) cpu_start: cpu freq: 160000000
I (194) cpu_start: Application information:
I (199) cpu_start: Project name:     hello-world
I (204) cpu_start: App version:      1
I (208) cpu_start: Compile time:     Jan 22 2022 13:29:43
I (214) cpu_start: ELF file SHA256:  0e2c68acd1a2e5a3...
I (220) cpu_start: ESP-IDF:          v4.3.2
I (226) heap_init: Initializing. RAM available for dynamic allocation:
I (233) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (239) heap_init: At 3FFB3210 len 0002CDF0 (179 KiB): DRAM
I (245) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (251) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (258) heap_init: At 4008B2CC len 00014D34 (83 KiB): IRAM
I (265) spi_flash: detected chip: gd
I (268) spi_flash: flash io: dio
W (272) spi_flash: Detected size(4096k) larger than the size in the binary image header(2048k). Using the size in the binary image header.
I (286) cpu_start: Starting scheduler on PRO CPU.
I (0) cpu_start: Starting scheduler on APP CPU.
Hello world!
This is esp32 chip with 2 CPU core(s), WiFi/BT/BLE, silicon revision 1, 2MB embedded flash
Minimum free heap size: 291312 bytes
Restarting in 10 seconds...
Restarting in 9 seconds...
Restarting in 8 seconds...
Restarting in 7 seconds...
Restarting in 6 seconds...
Restarting in 5 seconds...
Restarting in 4 seconds...
```
