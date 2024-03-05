export CXXFLAGS+=" -ffat-lto-objects"

OPTS+=" -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release -DALLOW_EXTERNAL_SPIRV_TOOLS=ON -DCMAKE_INSTALL_LIBDIR=lib -Wno-dev"

cmake -B $MODULE-static -G Ninja -DBUILD_SHARED_LIBS=OFF $OPTS &&
cmake --build $MODULE-static &&

cmake -B $MODULE-shared -G Ninja -DBUILD_SHARED_LIBS=ON -DGLSLANG_TESTS=ON $OPTS &&
cmake --build $MODULE-shared

prepare_install &&
cmake --install $MODULE-static &&
cmake --install $MODULE-shared
