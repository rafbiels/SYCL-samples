FROM ubuntu:22.04

# Get basic dependencies from Ubuntu repositories
RUN apt update && apt -y install wget gpg sudo git lshw vim cmake \
    gcc-11 gcc-12 libstdc++-11-dev libstdc++-12-dev libsdl2-dev \
    && apt clean

# Install Intel oneAPI repositories
RUN wget -O- https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB \
    | gpg --dearmor | tee /usr/share/keyrings/oneapi-archive-keyring.gpg > /dev/null \
    && echo "deb [signed-by=/usr/share/keyrings/oneapi-archive-keyring.gpg] https://apt.repos.intel.com/oneapi all main" \
    | tee /etc/apt/sources.list.d/oneAPI.list

# Install DPC++
RUN apt update && apt -y install intel-oneapi-compiler-dpcpp-cpp-2023.2.1 \
    && apt clean \
    && echo "source /opt/intel/oneapi/setvars.sh --include-intel-llvm" >> /root/.bashrc

# Set up entry point
ENTRYPOINT []
CMD /bin/bash

