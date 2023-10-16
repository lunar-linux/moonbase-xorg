OPTS+=" -DSPIRV_WERROR=OFF \
        -DBUILD_SHARED_LIBS=ON \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DCMAKE_INSTALL_LIBDIR=lib \
        -DCMAKE_BUILD_TYPE=Release \
        -DSPIRV_TOOLS_BUILD_STATIC=OFF \
        -DSPIRV-Headers_SOURCE_DIR=/usr"

cmake -B $MODULE-$VERSION -G Ninja $OPTS &&
ninja -C $MODULE-$VERSION &&

prepare_install &&
ninja -C $MODULE-$VERSION install
