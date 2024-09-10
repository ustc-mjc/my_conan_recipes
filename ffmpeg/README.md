# this is a conan recipe for building ffmpeg on all platforms
## build for Android
- use h264
- use mp3
- use fdk-aac
- enable-bsf=aac_adtstoasc
- --enable-bsf=h264_mp4toannexb
common args:
    CONFIGURE_FLAGS=--disable-shared \
    --enable-static \
    --disable-stripping \
    --disable-ffmpeg \
    --disable-ffplay \
    --disable-ffserver \
    --disable-ffprobe \
    --disable-avdevice \
    --disable-devices \
    --disable-indevs \
    --disable-outdevs \
    --disable-debug \
    --disable-asm \
    --disable-yasm \
    --disable-doc \
    --enable-small \
    --enable-dct \
    --enable-dwt \
    --enable-lsp \
    --enable-mdct \
    --enable-rdft \
    --enable-fft \
    --enable-version3 \
    --enable-nonfree \
    --disable-filters \
    --disable-postproc \
    --disable-bsfs \
    --enable-bsf=aac_adtstoasc \
    --enable-bsf=h264_mp4toannexb \
    --disable-encoders \
    --enable-encoder=pcm_s16le \
    --enable-encoder=aac \
    --enable-encoder=libvo_aacenc \
    --disable-decoders \
    --enable-decoder=aac \
    --enable-decoder=mp3 \
    --enable-decoder=pcm_s16le \
    --disable-parsers \
    --enable-parser=aac   \
    --disable-muxers \
    --enable-muxer=flv \
    --enable-muxer=wav \
    --enable-muxer=adts \
    --disable-demuxers \
    --enable-demuxer=flv \
    --enable-demuxer=wav \
    --enable-demuxer=aac \
    --disable-protocols \
    --enable-protocol=rtmp \
    --enable-protocol=file \
    --enable-libfdk_aac \
    --enable-libx264 \
    --enable-cross-compile \
    --prefix=$INSTALL_DIR

android args:
    ANDROID_NDK_ROOT=/Users/apple/soft/android/android-ndk-r9b
    PREBUILT=$ANDROID_NDK_ROOT/toolchains/arm-linux-androideabi-4.8/prebuilt/darwin-x86_64
    PLATFORM=$ANDROID_NDK_ROOT/platforms/android-8/arch-arm
    ./configure \
    $CONFIGURE_FLAGS \
    --target-os=linux \
    --arch=arm \
    --cross-prefix=$PREBUILT/bin/arm-linux-androideabi- \
    --sysroot=$PLATFORM \
    --extra-cflags="-marm -march=armv7-a -Ifdk_aac/include -Ix264 /include" \
    --extra-ldflags="-marm -march=armv7-a -Lfdk_aac/lib -Lx264 /lib"
