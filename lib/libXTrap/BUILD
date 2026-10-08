. /etc/profile.d/x11r7.rc &&

sed -i 's/typedef void (\*void_function)();/typedef void (*void_function)(void *tc, void *pdatum, void *userp);/' \
    /usr/include/X11/extensions/xtrapdi.h

default_build
