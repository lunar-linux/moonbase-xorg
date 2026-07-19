#DEPRECATION: Option 'glvnd' value 'true' is replaced by 'enabled'
OPTS+=" --optimization 2 \
        -D android-libbacktrace=disabled \
        -D b_lto=false \
        -D sysprof=false \
        -D build-tests=false \
        -D b_ndebug=true \
        -D platforms=auto \
        -D egl-native-platform=auto \
        -D shader-cache=auto \
        -D glx=auto \
        -D gbm=enabled \
        -D egl=enabled \
        -D gles2=enabled \
        -D gles1=disabled \
        -D glvnd=enabled \
        -D intel-rt=enabled \
        -D valgrind=disabled \
        -D html-docs=disabled \
        -D libunwind=disabled \
        -D shared-glapi=enabled \
        -D microsoft-clc=disabled \
        -D vulkan-drivers=auto \
        -D vulkan-layers=device-select,intel-nullhw,overlay,screenshot,anti-lag,vram-report-limit \
        -D video-codecs=all \
        -D gallium-drivers=auto \
        -D gallium-va=enabled \
        -D gallium-extra-hud=true \
        -D gallium-va=enabled \
        -D gallium-rusticl-enable-drivers=auto \
        -D vulkan-manifest-per-architecture=false \
        -D gallium-rusticl=true \
        -D llvm=enabled"

default_meson_build &&

# indirect rendering
ln -sf /usr/lib/libGLX_mesa.so.0 /usr/lib/libGLX_indirect.so.0
