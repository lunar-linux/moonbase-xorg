(

  # Mesa Gallium mklib breaks build when linker flags are set
  if [[ $GALLIUM == y ]]; then
    bad_flags linker
  fi  &&

  # Do not look for old libva
  sedit 's/libva = 0.31.1/libva = 0.32.0/' configure &&
  patch_it $SOURCE2 1 &&

  OPTS+=" --with-dri-drivers=$(echo $MESADRIVER | sed s/\ /,/g)"

  OPTS+=" --with-gallium-drivers=$(echo $GALLIUMDRIVER | sed s/\ /,/g)"

  if [[ $GALLIUM == y ]] && [[ $EGL == y ]]; then
    OPTS+=" --enable-gallium-egl"
  fi

  if module_installed xorg-server; then
    OPTS+=" --with-x --enable-xorg"
  fi  &&

  ./configure --prefix=/usr $OPTS &&
  make all  &&
  prepare_install  &&
  make install

) > $C_FIFO 2>&1
