# Build RTEMS

## 

    mkdir ~/Projects/rtems
    cd ~/Projects/rtems
    git clone git://git.rtems.org/rtems-source-builder.git rsb
    cd rsb
    git checlout 6
    ./source-builder/sb-check
    cd rtems
    ../source-builder/sb-set-builder --list-bsets

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

    git clone git://git.rtems.org/rtems.git rtems

    export PATH=$HOME/development/rtems/6/bin:$PATH 
    cd rtems
    ./bootstrap -c && ./rtems-bootstrap

    cd ..
    mkdir xilinx_zynq_a9_qemu
    cd xilinx_zynq_a9_qemu

~/Projects/rtems/kernel/rtems/configure --prefix=/home/eshan/development/rtems/5 --enable-maintainer-mode --target=arm-rtems6 --enable-rtemsbsp=xilinx_zynq_a9_qemu --enable-tests --enable-posix --disable-networking --enable-cxx

$ make -j 2
$ make install
