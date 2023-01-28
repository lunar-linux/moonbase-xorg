. /etc/profile.d/x11r7.rc

OPTS+=" --disable-static --enable-xkb --enable-xinput"

default_config &&
sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool &&
default_make
