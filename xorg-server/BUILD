  . /etc/profile.d/x11r7.rc  &&

  if [ -h /usr/share/X11/xkb/compiled ]; then
    rm -f /usr/share/X11/xkb/compiled
  fi  &&

  OPTS+=" --enable-dri          \
          --enable-dmx          \
          --enable-kdrive       \
          --enable-kdrive-evdev \
          --enable-kdrive-kbd   \
          --enable-kdrive-mouse \
          --enable-xcsecurity   \
          --enable-config-udev  \
          --enable-composite    \
          --disable-xfake       \
          --disable-static      \
          --disable-devel-docs  \
          --enable-install-libxf86config \
          --with-fontrootdir=/usr/share/fonts/X11" &&

  default_build  &&

  # This should not be needed, check in next release if still needed.
  rm -fr /usr/share/X11/xkb/compiled  &&
  mkdir -p /var/lib/xkb  &&
  ln -sf /var/lib/xkb /usr/share/X11/xkb/compiled &&

  # Fixes warning: "The directory "/usr/share/fonts/X11/OTF/" does not exist." in Xorg log.
  # This path looks to be hardcoded in Xorg server so let's create empty dir to workaround it.
  mkdir -p /usr/share/fonts/X11/OTF &&
  if  module_installed mkfontdir ; then
    mkfontdir /usr/share/fonts/X11/OTF
  fi
