. /etc/profile.d/x11r7.rc &&

if [ -h /usr/share/X11/xkb/compiled ]; then
  rm -f /usr/share/X11/xkb/compiled
fi &&

export CFLAGS=${CFLAGS/-fno-plt}
export CXXFLAGS=${CXXFLAGS/-fno-plt}
export LDFLAGS=${LDFLAGS/-Wl,-z,now}

OPTS+=" -Ddri1=auto        \
        -Ddri2=auto        \
        -Ddri3=auto        \
        -Ddrm=true         \
        -Dxorg=true        \
        -Dxcsecurity=true  \
        -Dudev=true        \
        -Dglamor=true      \
        -Ddocs=false       \
        -Dxkb_dir=/usr/share/X11/xkb \
        -Dxkb_output_dir=/var/lib/xkb \
        -Ddefault_font_path=/usr/share/fonts/"

default_meson_build

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

mkdir -p /etc/X11/xorg.conf.d
