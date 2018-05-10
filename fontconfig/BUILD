# We need to clear the cache dir or otherwise the build is going to fail
if [ -d /var/cache/fontconfig ]; then
  rm -f /var/cache/fontconfig/*
fi &&

# There is a documented issue when the user does not have a
# timezone set (/etc/localtime). It creates invalid XML
# syntax in a comment located in /etc/fonts/fonts.conf.
sedit "s:\`date\`::" configure  &&

OPTS+=" --with-templatedir=/etc/fonts/conf.avail \
        --with-default-fonts=/usr/share/fonts \
        --with-add-fonts=/usr/share/fonts \
        --with-xmldir=/etc/fonts \
        --disable-static" &&

default_build &&

install -m644 $SCRIPT_DIRECTORY/10-lunar-fonts.conf /etc/fonts/conf.d/