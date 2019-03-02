OPTS+=" --prefix /usr \
        -D udev=true \
        -D cairo-tests=false"

# if the  string is not empty
if [[ -n "${DRMDRIVER/[  ]*\n/}" ]]; then
   OPTS+=" -D"
   OPTS+=" $(echo $DRMDRIVER" " | sed 's:\ :=true -D :g')"
   OPTS+=" libkms=true"
fi

default_meson_build
