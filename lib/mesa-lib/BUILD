bad_flags linker

OPTS+=" -D b_lto=true \
        -D b_ndebug=true \
        -D platforms=x11,wayland \
        -D vulkan-drivers=auto \
        -D shader-cache=auto \
        -D video-codecs=vc1dec,h264dec,h264enc,h265dec,h265enc \
        -D gallium-drivers=auto \
        -D glx=dri \
        -D gbm=enabled \
        -D egl=enabled \
        -D dri3=enabled \
        -D gles2=enabled \
        -D gles1=disabled \
        -D glvnd=true \
        -D valgrind=disabled \
        -D shared-glapi=enabled \
        -D libunwind=enabled \
        -D gallium-va=enabled \
        -D gallium-xa=enabled \
        -D gallium-nine=true \
        -D gallium-vdpau=enabled \
        -D gallium-extra-hud=true \
        -D gallium-opencl=disabled \
        -D gallium-omx=bellagio \
        -D gallium-opencl=icd \
        -D gallium-va=enabled \
        -D microsoft-clc=disabled \
        -D llvm=enabled \
        -D osmesa=true"

default_meson_build &&

# indirect rendering
ln -sf /usr/lib/libGLX_mesa.so.0 /usr/lib/libGLX_indirect.so.0
