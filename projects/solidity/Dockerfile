# Copyright 2018 Google Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
################################################################################

FROM gcr.io/oss-fuzz-base/base-builder
RUN apt-get update && apt-get install -y make autoconf automake libtool \
    build-essential cmake libbz2-dev ninja-build zlib1g-dev wget
RUN git clone --recursive https://github.com/ethereum/solidity.git solidity
RUN git clone --depth 1 https://github.com/ethereum/solidity-fuzzing-corpus.git
RUN git clone --recursive -b boost-1.69.0 https://github.com/boostorg/boost.git boost
RUN git clone --depth 1 https://github.com/google/libprotobuf-mutator.git
RUN (mkdir LPM && cd LPM && cmake ../libprotobuf-mutator -GNinja -DLIB_PROTO_MUTATOR_DOWNLOAD_PROTOBUF=ON -DLIB_PROTO_MUTATOR_TESTING=OFF -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX="/usr" && ninja && ninja install && cd external.protobuf && cp -Rf bin lib include /usr)
RUN git clone --branch="v0.1.0" --recurse-submodules https://github.com/ethereum/evmone.git
RUN git clone --branch="v0.2.0" https://github.com/chfast/intx.git
RUN git clone --branch="v0.4.4" https://github.com/chfast/ethash.git
RUN (wget https://github.com/Kitware/CMake/releases/download/v3.14.5/cmake-3.14.5-Linux-x86_64.sh && chmod +x cmake-3.14.5-Linux-x86_64.sh && mkdir -p /src/cmake-3.14.5 && ./cmake-3.14.5-Linux-x86_64.sh --skip-license --prefix="/src/cmake-3.14.5")
COPY build.sh $SRC/
