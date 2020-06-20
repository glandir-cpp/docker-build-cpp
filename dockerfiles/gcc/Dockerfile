FROM debian:bullseye-slim

LABEL description="C++ compilation environment containing cmake and gcc/g++."

WORKDIR /usr/src
ENV CC=gcc-9
ENV CXX=g++-9

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
  cmake                                  \
  gcc-9                                  \
  g++-9                                  \
  make                                   \
  && rm -rf /var/lib/apt/lists/*
