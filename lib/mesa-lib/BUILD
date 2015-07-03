  NOCONFIGURE=1 ./autogen.sh &&

  if [[ $GALLIUM == y ]]; then
    # Mesa Gallium mklib breaks build when linker flags are set
    bad_flags linker &&
    OPTS+=" --with-gallium-drivers=swrast,$(echo $GALLIUMDRIVER | sed s/\ /,/g)" &&
    OPTS+=" --enable-gallium-egl --enable-gallium-osmesa"
  else
    OPTS+=" --enable-egl --enable-osmesa --with-gallium-drivers="
  fi  &&

  OPTS+=" --enable-dri  \
          --enable-dri3 \
          --with-dri-drivers=swrast,$(echo $MESADRIVER | sed s/\ /,/g)" &&

  OPTS+=" --enable-xa  \
          --enable-gbm \
          --enable-glx \
          --enable-gles1 \
          --enable-gles2 \
          --enable-shared-glapi \
          --with-egl-platforms=drm,x11" &&

  default_build
