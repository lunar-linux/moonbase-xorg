. /etc/profile.d/x11r7.rc &&

if [ -h /usr/share/X11/xkb/compiled ]; then
  rm -f /usr/share/X11/xkb/compiled
fi &&

export CFLAGS=${CFLAGS/-fno-plt}
export CXXFLAGS=${CXXFLAGS/-fno-plt}
export LDFLAGS=${LDFLAGS/,-z,now}

OPTS+=" -Dxorg=true \
        -Ddmx=false \
        -Dxwin=false \
        -Dxvfb=true \
        -Dxnest=false \
        -Dxephyr=false \
        -Dpciaccess=true \
        -Dxcsecurity=true \
        -Dxkb_default_rules=kbd \
        -Dxkb-output=/var/lib/xkb \
        -Dxkb_dir=/usr/share/X11/xkb \
        -Ddefault_font_path=/usr/share/fonts/"

#if ! module_installed udev; then
#   OPTS+=" -Dudev=false"
#fi

default_meson_build &&

# This should not be needed, check in next release if still needed.
rm -fr /usr/share/X11/xkb/compiled &&
mkdir -p /var/lib/xkb &&
ln -sf /var/lib/xkb /usr/share/X11/xkb/compiled &&

# Fixes warning: "The directory "/usr/share/fonts/X11/OTF/" does not exist." in Xorg log.
# This path looks to be hardcoded in Xorg server so let's create empty dir to workaround it.
mkdir -p /usr/share/fonts/X11/OTF &&
if module_installed mkfontdir; then
  mkfontdir /usr/share/fonts/X11/OTF
fi &&

if [[ "$ENABLE_WRAPPER" = "y" ]]; then
   # SUID on Xorg to allow user to start it
   chmod u+s "/usr/bin/Xorg"
fi &&

mkdir -p /etc/X11/xorg.conf.d
