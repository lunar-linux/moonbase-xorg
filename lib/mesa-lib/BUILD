(

  NOCONFIGURE=1 ./autogen.sh &&

  # Mesa Gallium mklib breaks build when linker flags are set
  if [[ $GALLIUM == y ]]; then
    bad_flags linker
  fi  &&

  OPTS+=" --with-dri-drivers=$(echo $MESADRIVER | sed s/\ /,/g)" &&

  OPTS+=" --with-gallium-drivers=$(echo $GALLIUMDRIVER | sed s/\ /,/g)" &&

  if [[ $GALLIUM == y ]] && [[ $EGL == y ]]; then
    OPTS+=" --enable-gallium-egl"
  fi &&

  default_build

) > $C_FIFO 2>&1
