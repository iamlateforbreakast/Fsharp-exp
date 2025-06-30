Uploading baremetal payload
https://forum.microchip.com/s/topic/a5CV40000001RNxMAM/t396475

Your understanding is on the right track. I'd like to expand on a few points to further clarify:
1. JTAG can only be used to program the embedded non-volatile memory (eNVM) not other memories e.g. eMMC.
2. For programming eMMC, SD, or QSPI on the board, the use of the HSS and a USB interface is generally required.
3. However, it's worth noting that you can program an SD card using a desktop PC and then insert it directly into the board's SD card slot. This method bypasses the need for a USB mass storage path through the HSS.
4. The 5-second wait time associated with the HSS is primarily due to the DDR training process that the HSS performs to initialize LPDDR4 memory. Once this is complete, loading the payload from eMMC, SD, or QSPI is significantly faster.
5. Keep in mind that if your payload.bin (which could be application code or a second-stage bootloader) is stored on eMMC, SD, or QSPI, the HSS is essential for execution. The HSS acts similarly to a First Stage Boot Loader (FSBL) and is equipped to read the payload from persistent storage devices.


P.S. The HSS also supports the YMODEM protocol to transfer data via the MMUART0 port. However, this method is considerably slower compared to the USB interface.

Creating a customize HSS bootloader
https://github.com/polarfire-soc/hart-software-services/tree/master/tools/hss-payload-generator

Load 2 RTOS ELF file in AMP configuration with HSS
https://github.com/polarfire-soc/polarfire-soc-amp-examples/tree/main

https://docs.rtems.org/docs/main/user/bsps/bsps-riscv.html

## Install SoftConsole

## Install Renode

## Compile RTEMS for RISCV

## Execute RTEMS example on Renode

arm-rtems4.9-objcopy -R -S -O binary hello.exe hello.bin

When working with U-Boot, it is also necessary to create an image file for U-Boot using the mkimage command. This involves specifying the architecture, operating system, type of image, compression, load address, entry point, and the binary file to be used. An example command is mkimage -A arm -O rtems -T kernel -C none -a 0x30000100 -e 0x30000100 -n "RTEMS Application" -d hello.bin hello.img.

## Connect to Renode execution with GDB

