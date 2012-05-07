(

 # Mesa Gallium mklib breaks build when linker flags are set
 if [[ $GALLIUM == y ]]; then
 bad_flags linker
 fi  &&

 # Do not look for old libva
 sedit 's/libva = 0.31.1/libva = 0.32.0/' configure &&
 patch_it $SOURCE2 1 &&

 # EGL is for embedded use only when needed by deps later
  OPTS+=" --disable-egl"  &&

  # Detect VMware VGA virtual 3D card and add driver for it
  VGA=`lspci | grep 'VGA.*VMware.*SVGA.*'`
  if [[ -n $VGA  ]]; then
     GALLIUMDRIVER+=" svga"
  fi  &&

  if [[ -n $MESADRIVER ]] ; then
    # Build selected drivers only, rather than the default of all of them
    # Ensure that swrast is included, as a fall-back
    OPTS+=" --with-dri-drivers=swrast,"
    OPTS+=$(echo $MESADRIVER | sed s/\ /,/g)
  fi  &&

  if [[ $GALLIUM == y ]]; then
    OPTS+=" --enable-gallium-llvm --enable-egl --enable-gallium-egl --enable-openvg --enable-xa --enable-gallium-g3dvl"
    if module_installed libXvMC; then
       OPTS+=" --enable-xvmc"
    fi
    if module_installed libvdpau; then
       OPTS+=" --enable-vdpau"
    fi
    if module_installed libva; then
       OPTS+=" --enable-va"
    fi
    if [[ -n $GALLIUMDRIVER ]]; then
    OPTS+=" --with-gallium-drivers=swrast,"
    OPTS+=$(echo $GALLIUMDRIVER | sed s/\ /,/g)
    fi
  else OPTS+=" --disable-gallium-llvm "
  fi  &&

  if ! module_installed llvm && [[ $GALLIUMDRIVER == *r[36]00* ]] || [[ $GALLIUMDRIVER == "" ]]; then
  message "$PROBLEM_COLOR You have selected all GPU drivers or Radeon,"
  message "but llvm module is NOT installed."
  message "Install llvm module or do not choose all or Radeon drivers $DEFAULT_COLOR"
  exit 1
  else sedit 's/^GALLIUM_DRIVERS_DEFAULT=.*/GALLIUM_DRIVERS_DEFAULT="swrast"/' configure
  fi  &&

  if module_installed xorg-server; then
     OPTS+=" --with-x --enable-xorg"
  fi  &&

  ./configure --prefix=/usr $OPTS &&

  prepare_install  &&

  make all  &&

  make install

) > $C_FIFO 2>&1
