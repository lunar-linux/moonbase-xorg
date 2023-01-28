OPTS+=" -DSPIRV_WERROR=Off \
        -DBUILD_SHARED_LIBS=ON \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DCMAKE_INSTALL_LIBDIR=lib \
        -DCMAKE_BUILD_TYPE=Release \
        -DBUILD_SHARED_LIBS=ON \
        -DSPIRV_TOOLS_BUILD_STATIC=OFF \
        -DSPIRV-Headers_SOURCE_DIR=/usr "

default_cmake_build &&

cd ../
install -dm755 include/spirv-tools/ /usr/include/spirv-tools
