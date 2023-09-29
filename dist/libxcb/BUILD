export LANG=en_US.UTF-8

. /etc/profile.d/x11r7.rc

./autogen.sh &&

OPTS+=" --disable-devel-docs --without-doxygen --disable-static --enable-xkb --enable-xinput"

default_config &&
sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool &&
default_make
