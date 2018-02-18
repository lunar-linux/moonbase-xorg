mkdir build &&

cd build &&

meson --prefix /usr \
      -Denable-glx=yes \
      $OPTS && 

ninja &&

prepare_install &&

ninja install
