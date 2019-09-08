# Copyright (c) 2017, 2019 IBM Corp. and others
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
#   docker build -t=openj9-jdk8 .
#   docker run --name=jdk8 -it openj9-jdk8

FROM ubuntu:18.04

# Install the required tools.
RUN apt-get update \
 && apt-get install -qq -y --no-install-recommends \
	  autoconf \
	  ca-certificates \
	  ccache \
	  cmake \
	  cpio \
	  file \
	  g++-4.8 \
	  gcc-4.8 \
	  git \
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
      software-properties-common \
	  ssh \
	  unzip \
	  wget \
	  zip \
 && rm -rf /var/lib/apt/lists/*

# Install optional tools.
RUN apt-get update \
 && apt-get install -qq -y --no-install-recommends \
	  less \
	  vim \
 && rm -rf /var/lib/apt/lists/*

# Create links to the required compiler version.
RUN ln -s gcc-4.8 /usr/bin/cc \
 && ln -s gcc-4.8 /usr/bin/gcc \
 && ln -s g++-4.8 /usr/bin/c++ \
 && ln -s g++-4.8 /usr/bin/g++

# Download and unpack freemarker.
RUN cd /root \
 && wget https://sourceforge.net/projects/freemarker/files/freemarker/2.3.8/freemarker-2.3.8.tar.gz/download -O freemarker.tar.gz \
 && tar -xzf freemarker.tar.gz freemarker-2.3.8/lib/freemarker.jar --strip=2 \
 && rm -f freemarker.tar.gz

# Download the boot JDK from AdoptOpenJDK.
RUN cd /root \
 && wget https://140-211-168-230-openstack.osuosl.org/artifactory/ci-eclipse-openj9/Build_JDK8_x86-64_linux_Personal/293/OpenJ9-JDK8-x86-64_linux-20190906-184840.tar.gz \
 && tar -xzf OpenJ9-JDK8-x86-64_linux-*.tar.gz \
 && rm -f OpenJ9-JDK8-x86-64_linux-*.tar.gz 
RUN cd /root && mv j2sdk-image bootjdk8 
# Set JAVA_HOME, and prepend $JAVA_HOME/bin to PATH.
ENV JAVA_HOME=/root/bootjdk8
ENV PATH="$JAVA_HOME/bin:$PATH"

WORKDIR /root
