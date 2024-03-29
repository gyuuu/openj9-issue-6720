# Copyright (c) 2018, 2019 IBM Corp. and others
#
# This program and the accompanying materials are made available under
# the terms of the Eclipse Public License 2.0 which accompanies this
# distribution and is available at https://www.eclipse.org/legal/epl-2.0/
# or the Apache License, Version 2.0 which accompanies this distribution and
# is available at https://www.apache.org/licenses/LICENSE-2.0.
#
# This Source Code may also be made available under the following
# Secondary Licenses when the conditions for such availability set
# forth in the Eclipse Public License, v. 2.0 are satisfied: GNU
# General Public License, version 2 with the GNU Classpath
# Exception [1] and GNU General Public License, version 2 with the
# OpenJDK Assembly Exception [2].
#
# [1] https://www.gnu.org/software/classpath/license.html
# [2] http://openjdk.java.net/legal/assembly-exception.html
#
# SPDX-License-Identifier: EPL-2.0 OR Apache-2.0 OR GPL-2.0 WITH Classpath-exception-2.0 OR LicenseRef-GPL-2.0 WITH Assembly-exception

# To use this docker file:
#   docker build -t=openj9 .
#   docker run -it openj9

FROM ubuntu:16.04

# Install required OS tools
RUN apt-get update \
  && apt-get install -qq -y --no-install-recommends \
    software-properties-common \
    python-software-properties \
  && apt-get update \
  && apt-get install -qq -y --no-install-recommends \
    autoconf \
    ca-certificates \
    ccache \
    cmake \
    cpio \
    file \
    git \
    git-core \
    libasound2-dev \
    libcups2-dev \
    libdwarf-dev \
    libelf-dev \
    libfontconfig1-dev \
    libfreetype6-dev \
    libnuma-dev \
    libx11-dev \
    libxext-dev \
    libxrender-dev \
    libxt-dev \
    libxtst-dev \
    make \
    nasm \
    pkg-config \
    realpath \
    ssh \
    unzip \
    wget \
    zip \
    vim \
  && rm -rf /var/lib/apt/lists/*

# Add the GCC-7.3 Binary
RUN cd /usr/local \
  && wget -O gcc-7.tar.xz "https://ci.adoptopenjdk.net/userContent/gcc/gcc730+ccache.x86_64.tar.xz" \
  && tar -xJf gcc-7.tar.xz --strip-components=1 \
  && rm -rf gcc-7.tar.xz

# Create links for GCC to access the C library and gcc,g++
RUN ln -s /usr/lib/x86_64-linux-gnu /usr/lib64 \
  && ln -s /usr/include/x86_64-linux-gnu/* /usr/local/include \
  && ln -s /usr/local/bin/g++-7.3 /usr/bin/g++ \
  && ln -s /usr/local/bin/gcc-7.3 /usr/bin/gcc

# Download and setup freemarker.jar to /root/freemarker.jar
RUN cd /root \
  && wget https://sourceforge.net/projects/freemarker/files/freemarker/2.3.8/freemarker-2.3.8.tar.gz/download -O freemarker.tgz \
  && tar -xzf freemarker.tgz freemarker-2.3.8/lib/freemarker.jar --strip=2 \
  && rm -f freemarker.tgz

# Download and install boot JDK from AdoptOpenJDK
RUN cd /root \
  && wget https://140-211-168-230-openstack.osuosl.org/artifactory/ci-eclipse-openj9/Build_JDK11_x86-64_linux_Personal/240/OpenJ9-JDK11-x86-64_linux-20190906-184832.tar.gz
RUN cd /root && tar -xzf OpenJ9-JDK11-x86-64_linux-*.tar.gz \
  && rm -f OpenJ9-JDK11-x86-64_linux-*.tar.gz
RUN cd /root && mv jdk bootjdk11

# Set environment variable JAVA_HOME, and prepend ${JAVA_HOME}/bin to PATH
ENV JAVA_HOME="/root/bootjdk11"
ENV PATH="${JAVA_HOME}/bin:${PATH}"

WORKDIR /root