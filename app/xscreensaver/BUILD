  # Now let's do the PAM stuff the proper way
  if module_installed Linux-PAM; then
    OPTS+=" --with-pam --without-shadow"
  fi  &&

  OPTS+=" --prefix=/usr           \
          --without-kerberos      \
          --with-dpms-ext         \
          --with-xf86vmode-ext    \
          --with-xf86gamma-ext    \
          --without-gle           \
          --with-proc-interrupts  \
          --with-pthread          \
          --with-xshm-ext         \
          --disable-nls           \
          --enable-locking"      &&

  default_build
