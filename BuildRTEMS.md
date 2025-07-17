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

    ../source-builder/sb-set-builder --prefix=/home/eshan/development/rtems/6 6/rtems-arm

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

/home/eshan/development/rtems/kernel/rtems/configure --prefix=/home/eshan/development/rtems/5 --enable-maintainer-mode --target=arm-rtems5 --enable-rtemsbsp=xilinx_zynq_a9_qemu --enable-tests --enable-posix --disable-networking --enable-cxx

$ make -j 2
$ make install
