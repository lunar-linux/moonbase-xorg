bad_flags linker

OPTS+=" -Db_lto=false \
        -Db_ndebug=true \
        -Dplatforms=x11,drm,wayland,surfaceless \
        -Ddri-drivers=i915,i965,r100,r200,nouveau \
        -Dgallium-drivers=r300,r600,radeonsi,nouveau,virgl,svga,swrast,swr,iris \
        -Dvulkan-drivers=amd,intel \
        -Dglx=dri \
        -Dgbm=true \
        -Degl=true \
        -Ddri3=true \
        -Dgles1=false \
        -Dgles2=true \
        -Dvalgrind=false \
        -Dshared-glapi=true \
        -Dswr-arches=avx,avx2 \
        -Dglvnd=true \
        -Dlibunwind=true \
        -Dgallium-xvmc=false \
        -Dgallium-va=true \
        -Dgallium-extra-hud=true \
        -Dgallium-xa=true \
        -Dgallium-nine=true \
        -Dgallium-opencl=disabled \
        -Dllvm=true \
        -Dosmesa=gallium"

default_meson_build &&

# indirect rendering
ln -s /usr/lib/libGLX_mesa.so.0 /usr/lib/libGLX_indirect.so.0
