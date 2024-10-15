FROM ubuntu

RUN apt update -y && DEBIAN_FRONTEND=noninteractive apt install -y wget gzip

RUN wget https://github.com/cloudflare/workerd/releases/download/v1.20241011.0/workerd-linux-64.gz
RUN gunzip workerd-linux-64.gz
RUN chmod +x workerd-linux-64

COPY ./samples/helloworld /helloworld

CMD ["/workerd-linux-64",  "serve", "/helloworld/config.capnp"]

## Bazel is complaining: unrecognized option: @rules_rust//:extra_rustc_flag

# FROM gcr.io/bazel-public/bazel:latest AS builder

# USER root

# RUN apt update -y && DEBIAN_FRONTEND=noninteractive apt install -y wget \
#                                                                     python3 \
#                                                                     python3-distutils \
#                                                                     tcl8.6 \
#                                                                     lsb-release \
#                                                                     software-properties-common \
#                                                                     gnupg
# RUN wget https://apt.llvm.org/llvm.sh
# RUN chmod +x ./llvm.sh
# RUN ./llvm.sh 16

# COPY . /work
# WORKDIR /work

# RUN bazel build //src/workerd/server:workerd

# # Pick an arbitrary sample to build; we'll pick hello-wasm
# WORKDIR ./samples/hello-wasm
# RUN workerd compile config.capnp > workerd-wasm

# FROM ubuntu
# COPY --from=builder /work/samples/hello-wasm/workerd-wasm /
