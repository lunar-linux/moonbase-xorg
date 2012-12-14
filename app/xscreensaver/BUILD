(

  # Now let's do the PAM stuff the proper way
  if module_installed Linux-PAM; then
    OPTS+=" --with-pam --without-shadow"
  fi  &&

  OPTS+=" --without-kerberos      \
          --with-dpms-ext         \
          --with-xf86vmode-ext    \
          --with-xf86gamma-ext    \
          --with-proc-interrupts  \
          --without-pixbuf        \
          --enable-locking"      &&

  # this is a harmless debugging line and AF_LINK is currently undefined over here
  sedit '/AF_LINK/d' hacks/glx/sonar-icmp.c &&
  # remove unnecessary #endif
  sedit '597d' hacks/glx/sonar-icmp.c &&

  default_build

) > $C_FIFO 2>&1
