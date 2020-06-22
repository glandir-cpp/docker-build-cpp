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

ENV MSAN_LIBCXX_PATH="/usr/src/libcxx_msan"
COPY build-libcxx_msan .
RUN ./build-libcxx_msan && rm build-libcxx_msan

