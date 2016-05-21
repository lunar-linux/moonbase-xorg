NOCONFIGURE=1 ./autogen.sh &&

if [[ $GALLIUM == y ]]; then
  # Mesa Gallium mklib breaks build when linker flags are set
  bad_flags linker &&
  OPTS+=" --with-gallium-drivers=swrast,$(echo $GALLIUMDRIVER | sed s/\ /,/g)" &&
  OPTS+=" --enable-gallium-egl --enable-gallium-osmesa"
else
  OPTS+=" --enable-egl --enable-osmesa --with-gallium-drivers="
fi  &&

if module_installed wayland; then
  OPTS+=" --with-egl-platforms=drm,x11,wayland"
   else
  OPTS+=" --with-egl-platforms=drm,x11"
fi &&

OPTS+=" --enable-dri   \
        --enable-dri3  \
        --enable-xa    \
        --enable-gbm   \
        --enable-glx   \
        --enable-gles1 \
        --enable-gles2 \
        --enable-shared-glapi \
        --enable-texture-float \
        --disable-omx \
        --disable-opencl \
        --disable-opencl-icd \
        --with-dri-drivers=swrast,$(echo $MESADRIVER | sed s/\ /,/g)" &&

default_build
