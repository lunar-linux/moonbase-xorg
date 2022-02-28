bad_flags linker

OPTS+=" -D b_lto=true \
        -D b_ndebug=true \
        -D platforms=x11,wayland \
        -D dri-drivers=i915,i965,r100,r200,nouveau \
        -D gallium-drivers=r300,r600,radeonsi,nouveau,virgl,svga,swrast,iris \
        -D vulkan-drivers=amd,intel,swrast \
        -D glx=dri \
        -D gbm=enabled \
        -D egl=enabled \
        -D dri3=enabled \
        -D gles2=enabled \
        -D gles1=disabled \
        -D glvnd=true \
        -D valgrind=disabled \
        -D shared-glapi=enabled \
        -D swr-arches=avx,avx2 \
        -D libunwind=enabled \
        -D gallium-va=enabled \
        -D gallium-xa=enabled \
        -D gallium-nine=true \
        -D gallium-vdpau=enabled \
        -D gallium-xvmc=disabled \
        -D gallium-extra-hud=true \
        -D gallium-opencl=disabled \
        -D microsoft-clc=disabled \
        -D libunwind=enabled \
        -D llvm=enabled \
        -D osmesa=true"

default_meson_build &&

# indirect rendering
ln -s /usr/lib/libGLX_mesa.so.0 /usr/lib/libGLX_indirect.so.0
