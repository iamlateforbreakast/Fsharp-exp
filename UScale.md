Using an ALinx Uscale+ board to connect to an AXI lite interface

https://www.hackster.io/mabushaqraedu0/axi-lite-slave-custom-ip-core-to-control-led-under-petalinux-b70b1d

ALinx Github including examples

https://github.com/alinxalinx/AXU2CG-E_AXU3EG_AXU4EV-E_AXU5EV-E

User Manual AXU3EGB

https://www.manualslib.com/manual/3069776/Alinx-ZynqultrascalePlus-Axu3egb.html

Booting message throught serial console
---------------------------------------

The typical sequence on the serial console is as follows:

1. First Stage Boot Loader (FSBL) Output

The process begins when power is applied. The BootROM loads and executes the FSBL (First Stage Boot Loader), which will output initial debug messages. 
Initial messages: You will see messages indicating the FSBL is running, potentially showing a version and build date.
Hardware initialization: Messages about basic hardware setup, such as:
CPU: Information on the specific ZynqMP CPU and Silicon version.
DRAM: Memory detection and configuration (e.g., "DRAM: 2 GiB").
Flash/MMC: Detection of QSPI flash and SD card interfaces.
FPGA programming (if applicable): If a bitstream is included in the BOOT.bin, the FSBL will program the FPGA, and you may see a message indicating this step.
Loading ATF and U-Boot: Messages indicating that the FSBL is loading the ARM Trusted Firmware (ATF/BL31) and the U-Boot bootloader from the boot device (e.g., SD card or QSPI flash) into memory. 

3. U-Boot Output

Once the FSBL hands off control to U-Boot, you will see a new set of messages. 
U-Boot banner: The U-Boot version and build information will be displayed (e.g., "U-Boot 2021.01 (Oct 12 2021 - 09:28:42 +0000)").
Hardware details: Further configuration details for the board's components.
Autoboot countdown: A message like "Hit any key to stop autoboot: X" will appear, counting down from a few seconds. Pressing a key will let you enter the U-Boot command prompt.
Boot media access: Messages related to accessing the boot media (e.g., "Loading Environment from SPIFlash...").
Loading Linux kernel and DTB: Messages confirming U-Boot is loading the Linux kernel image and the Device Tree Blob (DTB) from the SD card or QSPI flash into the DRAM (e.g., "Image Name: Linux Kernel Image", "Data Size: ...", "Booting kernel from Legacy Image at ...").
"Starting Kernel" message: U-Boot will display this message just before jumping to the kernel's entry point. After this, control is passed to the Linux kernel. 

4. Linux Kernel Output 

Once the kernel starts executing, it takes over the serial console. 
Linux banner: The kernel will print its own initial banner and version information (e.g., "Linux version 5.x.x ...").
Kernel initialization messages: A rapid stream of messages (the kernel ring buffer) detailing the initialization of various subsystems, drivers, and the detection of hardware, including:
CPU configuration (e.g., "Booting Linux on physical CPU 0")
Memory management setup.
Device driver initialization (e.g., for networking, storage, timers, etc.).
Mounting the initial RAM disk (initramfs) if used.
Setting up the serial console itself (e.g., "serial8250: ttyS0 at MMIO ...").
Filesystem mounting: Messages about mounting the root filesystem (from SD card, eMMC, or NFS). 

5. User Space (Init) Output

Finally, the kernel starts the initial user-space process (usually init or systemd), and you will see: 
System service startup: Messages about starting various system services.
Login prompt: The final message will be the user login prompt on the serial console, indicating the system is fully booted and ready for interaction. 
Common Issues to Watch For
No output after "Starting Kernel": This often means the kernel failed to boot (e.g., a kernel panic) before the serial console was properly initialized in the kernel phase, or the device tree is invalid.
Garbled output: This typically indicates a baud rate mismatch between your terminal software and the boot stage currently active. The common baud rate for Zynq systems is 115200 bps.
"Warning - bad CRC, using default environment": A message from U-Boot indicating the saved environment variables are corrupt, and it's using default settings. 
