mkdir build &&

cd build &&

meson --prefix /usr \
      -Dudev=true \
      -Damdgpu=auto \
      -Dfreedreno=auto \
      -Dexynos=auto \
      -Domap=auto \
      -Dtegra=auto \
      $OPTS && 

ninja &&

prepare_install &&

ninja install
