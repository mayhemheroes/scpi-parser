FROM --platform=linux/amd64 ubuntu:20.04 as builder

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y build-essential clang cmake g++

COPY . /repo
WORKDIR /repo
RUN make
WORKDIR /repo/mayhem/build
RUN CC=clang CXX=clang++ cmake ..
RUN make
#RUN ./fuzzparser ../CORPUS_DIR

FROM ubuntu:20.04 as package
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y libreadline-dev
COPY --from=builder /repo/mayhem/build/fuzzscpi-parser /fuzzscpi-parser
COPY --from=builder /repo/mayhem/CORPUS_DIR /testsuite
