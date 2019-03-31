. /etc/profile.d/x11r7.rc &&

OPTS+=" --disable-static"

default_build &&

install -m755 -d /usr/share/X11/xorg.conf.d &&
install -m644 $SCRIPT_DIRECTORY/90-libinput.conf /usr/share/X11/xorg.conf.d/
