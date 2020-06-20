FROM debian:bullseye-slim

LABEL description="C++ compilation environment containing cmake and clang."

WORKDIR /usr/src
ENV CC=clang-10
ENV CXX=clang++-10

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
	clang-10                             \
	cmake                                \
	make                                 \
  && rm -rf /var/lib/apt/lists/*
