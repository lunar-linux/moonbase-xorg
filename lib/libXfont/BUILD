(

  . /etc/profile.d/x11r7.rc  &&

  patch_it $SOURCE2 1 &&
  sedit "s:fontsproto <:fontsproto >=:" configure.ac &&
    
  OPTS+=" --disable-static --disable-devel-docs" &&

  autoreconf &&
  default_build

) > $C_FIFO 2>&1
