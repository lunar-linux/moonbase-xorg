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
          --without-pixbuf        \
          --with-proc-interrupts  \
          --with-pthread          \
          --with-xshm-ext         \
          --disable-nls           \
          --enable-locking"      &&

  # this is a harmless debugging line and AF_LINK is currently undefined over here
#  sedit '/AF_LINK/d' hacks/glx/sonar-icmp.c &&
  # remove unnecessary #endif
#  sedit '597d' hacks/glx/sonar-icmp.c &&

# Else it tanks on pthread stuff
  LIBS=-lpthread ./configure $OPTS &&

  default_make
