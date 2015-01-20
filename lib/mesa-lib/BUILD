  NOCONFIGURE=1 ./autogen.sh &&

  if [[ $GALLIUM == y ]]; then
    # Mesa Gallium mklib breaks build when linker flags are set
    bad_flags linker &&
    OPTS+=" --enable-gallium-egl --enable-gallium-osmesa"
  else
    OPTS+=" --enable-egl --enable-osmesa"
  fi  &&

  OPTS+=" --with-dri-drivers=$(echo $MESADRIVER | sed s/\ /,/g)" &&

  OPTS+=" --with-gallium-drivers=$(echo $GALLIUMDRIVER | sed s/\ /,/g)" &&

  OPTS+=" --enable-xa --enable-gles1 --enable-gles2 --enable-gbm --with-egl-platforms=drm,x11" &&

  default_build
