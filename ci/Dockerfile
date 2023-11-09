FROM ubuntu:22.04

# Get basic dependencies from Ubuntu repositories
RUN apt update && apt -y install wget gpg cmake \
    gcc-12 libstdc++-12-dev libsdl2-dev \
    && apt clean

# Install Intel oneAPI repositories
RUN wget -O- https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB \
    | gpg --dearmor | tee /usr/share/keyrings/oneapi-archive-keyring.gpg > /dev/null \
    && echo "deb [signed-by=/usr/share/keyrings/oneapi-archive-keyring.gpg] https://apt.repos.intel.com/oneapi all main" \
    | tee /etc/apt/sources.list.d/oneAPI.list

# Install DPC++ and remove parts we don't need to reduce the container size
RUN apt update && apt -y install intel-oneapi-compiler-dpcpp-cpp-2023.2.1 \
    && apt clean \
    && cd /opt/intel/oneapi \
    && rm -rf conda_channel debugger dev-utilities dpl compiler/latest/linux/lib/oclfpga

# Set up the environment
ENV ONEAPI_ROOT=/opt/intel/oneapi
ENV CMPLR_ROOT=${ONEAPI_ROOT}/compiler/latest
ENV PATH=${CMPLR_ROOT}/linux/bin-llvm:${CMPLR_ROOT}/linux/bin/intel64:${CMPLR_ROOT}/linux/bin:${PATH}
ENV CPATH=${CMPLR_ROOT}/linux/include:${CMPLR_ROOT}/linux/compiler/include:${CPATH}
ENV LIBRARY_PATH=${CMPLR_ROOT}/linux/lib:${CMPLR_ROOT}/linux/lib/x64:${CMPLR_ROOT}/linux/compiler/lib/intel64:${LIBRARY_PATH}
ENV LD_LIBRARY_PATH=${CMPLR_ROOT}/linux/lib:${CMPLR_ROOT}/linux/lib/x64:${CMPLR_ROOT}/linux/compiler/lib/intel64:${LD_LIBRARY_PATH}

# Set up entry point
ENTRYPOINT []
CMD /bin/bash
