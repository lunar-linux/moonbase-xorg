NOCONFIGURE=1 ./autogen.sh &&

if [[ $GALLIUM == y ]]; then
  # Mesa Gallium mklib breaks build when linker flags are set
  bad_flags linker &&
  OPTS+=" --with-gallium-drivers=swrast,$(echo $GALLIUMDRIVER | sed s/\ /,/g)" &&
  OPTS+=" --enable-gallium-osmesa" &&
  OPTS+=" --enable-llvm --enable-llvm-shared-libs --with-clang-libdir=/usr/lib"
else
  OPTS+=" --enable-gallium-osmesa --with-gallium-drivers=svga,swrast"
fi &&

OPTS+=" --with-platforms=drm,x11" &&
if in_depends $MODULE wayland-protocols; then
  OPTS+=",wayland"
fi &&

OPTS+=" --enable-xa \
        --enable-gbm \
        --enable-dri \
        --enable-egl \
        --enable-glx \
        --enable-dri3 \
        --enable-gles1 \
        --enable-gles2 \
        --enable-shared-glapi \
        --enable-texture-float \
        --disable-opencl \
        --disable-opencl-icd \
        --with-dri-drivers=swrast,$(echo $MESADRIVER | sed s/\ /,/g)" &&

default_build &&

# indirect rendering
ln -s /usr/lib/libGLX_mesa.so.0 /usr/lib/libGLX_indirect.so.0
