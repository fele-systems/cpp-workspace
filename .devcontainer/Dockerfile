FROM mcr.microsoft.com/devcontainers/cpp:0-debian-11

ARG REINSTALL_CMAKE_VERSION_FROM_SOURCE="3.27.2"

# Optionally install the cmake for vcpkg
COPY ./reinstall-cmake.sh /tmp/

RUN if [ "${REINSTALL_CMAKE_VERSION_FROM_SOURCE}" != "none" ]; then \
        chmod +x /tmp/reinstall-cmake.sh && /tmp/reinstall-cmake.sh ${REINSTALL_CMAKE_VERSION_FROM_SOURCE}; \
    fi \
    && rm -f /tmp/reinstall-cmake.sh

# [Optional] Uncomment this section to install additional vcpkg ports.
# RUN su vscode -c "${VCPKG_ROOT}/vcpkg install <your-port-name-here>"

# Install cool dependencies
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        libcapstone-dev libfmt-dev libpugixml-dev \
        clangd zsh

# Install conan
RUN wget -O conan-ubuntu-64.deb https://github.com/conan-io/conan/releases/download/2.4.1/conan-2.4.1-amd64.deb \
    && dpkg -i conan-ubuntu-64.deb \
    && rm conan-ubuntu-64.deb

# Change default shell to zsh
RUN chsh -s /usr/bin/zsh
