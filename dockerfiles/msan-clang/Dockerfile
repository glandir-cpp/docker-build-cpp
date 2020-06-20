FROM debian:bullseye-slim

LABEL description="C++ compilation environment containing cmake, clang and libcxx compiled with MSan."

WORKDIR /usr/src
ENV CC=clang-10
ENV CXX=clang++-10

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
	ca-certificates                      \
	clang-10                             \
	cmake                                \
	make                                 \
	git                                  \
	&& rm -rf /var/lib/apt/lists/*

RUN git clone --depth=1 https://github.com/llvm/llvm-project \
	&& mkdir /usr/src/libcxx_msan                            \
	&& cd /usr/src/libcxx_msan                               \
	&& cmake ../llvm-project/llvm                            \
		-DCMAKE_BUILD_TYPE=Release                           \
		-DLLVM_ENABLE_PROJECTS="libcxx;libcxxabi"            \
		-DLLVM_USE_SANITIZER=MemoryWithOrigins               \
	&& make -j4 cxx cxxabi                                   \
	&& rm -rf /usr/src/llvm-project

ENV MSAN_LIBCXX_PATH="/usr/src/libcxx_msan"
ENV MSAN_CFLAGS="-fsanitize=memory \
-stdlib=libc++ \
-L$MSAN_LIBCXX_PATH/lib \
-lc++abi \
-I$MSAN_LIBCXX_PATH/include \
-I$MSAN_LIBCXX_PATH/include/c++/v1"
ENV LDFLAGS="-fsanitize=memory"
ENV LD_LIBRARY_PATH='$MSAN_LIBCXX_PATH/lib/'
