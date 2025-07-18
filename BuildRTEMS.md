# Build RTEMS

## 

    mkdir ~/Projects/rtems
    cd ~/Projects/rtems
    git clone https://gitlab.rtems.org/rtems/tools/rtems-source-builder.git rsb
    cd rsb
    git branch -v -a to check all remotebranches
    git checkout 6
    cd source-builder
    ./source-builder/sb-check
    cd rtems
    ./source-builder/sb-set-builder --list-bsets

## Buid toolchain

    ../source-builder/sb-set-builder --prefix=~/Projects/rtems/6 6/rtems-arm
    
or

    ../source-builder/sb-set-builder --prefix=~/Projects/rtems/6 6/rtems-riscv
    
or

    ../source-builder/sb-set-builder --prefix=~/Projects/rtems/6 6/rtems-sparc

## Build kernel

    cd
    cd development/rtems
    mkdir kernel
    cd kernel

    git clone https://gitlab.rtems.org/rtems/rtos/rtems.git
    
    export PATH=$HOME/Proects/rtems/6/bin:$PATH 
    cd rtems
    ./waf configure --prefix=$HOME/rtems-start/rtems/6
    ./waf
    ./waf install

## Compile QEMU

    cd ..
    mkdir xilinx_zynq_a9_qemu
    cd xilinx_zynq_a9_qemu

~/Projects/rtems/kernel/rtems/configure --prefix=/home/eshan/development/rtems/5 --enable-maintainer-mode --target=arm-rtems6 --enable-rtemsbsp=xilinx_zynq_a9_qemu --enable-tests --enable-posix --disable-networking --enable-cxx

$ make -j 2
$ make install
