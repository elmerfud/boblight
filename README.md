# Boblight

This repo is for the Boblight project with updates needed to compile and run on Android.  

This has only been tested to work using the following:
- Android NDK r16b
- Nvidia Shield TV 2015 16GB

## Compiling

1. Download the NDK from google and unpack it.  Recommend using the version listed above.  Other versions may not work. 
1. Make the standalone tool chain for the NDK
    ```bash
    cd /<path to your NDK>
    ./build/tools/make-standalone-toolchain.sh --arch=arm64 --install-dir=<path where you want the tool chain>
    ```

1. Navigation to the path where you downloaded boblight
1. Setup shell variables we'll need to use our tool chain for cross compiling.
    ```bash
    export PATH=<path where you want the tool chain>/bin:$PATH
    export CC=aarch64-linux-android-clang
    export CXX=aarch64-linux-android-clang++
    export CFLAGS="-g -O2 -fPIE -DHAVE_PTHREADS"
    export CXXFLAGS="-g -O2 -fPIE -DHAVE_PTHREADS"
    export LDFLAGS="-fPIE -pie"
    ```
1. Configure and build boblight
    ```bash
    ./configure --host=aarch64-unknown-linux-gnu --without-portaudio --without-libusb --without-spi --without-x11 --without-opengl
    make
    ```
1. Your binary is at ./src/boblightd.  Transfer this to your Android device along with your config file.  
1. Set any required permissons to ensure the binary can run on Android and read the correct /dev device.
1. Run boblightd.
