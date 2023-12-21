FROM ubuntu:18.04

COPY ./ /gpdb_src/
# COPY greenplum-oss/sysconf.bash /gpdb_src/sysconf.bash
# COPY concourse/ /gpdb_src/concourse/

WORKDIR /
ENV DEBIAN_FRONTEND=noninteractive

RUN echo "/usr/local/lib" > /etc/ld.so.conf.d/usr-local.conf \
    && ldconfig

# Install gpdb dependencies
WORKDIR /gpdb_src
RUN chmod +x README.ubuntu.bash \
    && ./README.ubuntu.bash

# Build gp-xerces
WORKDIR /
RUN git clone --depth 1 --branch v3.1.2-p1 https://github.com/greenplum-db/gp-xerces.git
RUN mkdir /gp-xerces/build
WORKDIR /gp-xerces/build
RUN ../configure --prefix=/usr/local \
    && make \
    && make install

# Set up gpadmin user and sysconf stuff
WORKDIR /
RUN chmod +x gpdb_src/greenplum-oss/sysconf.bash \
    && gpdb_src/greenplum-oss/sysconf.bash
RUN chmod +x gpdb_src/concourse/scripts/setup_gpadmin_user.bash \
    && gpdb_src/concourse/scripts/setup_gpadmin_user.bash

# Configure build environment to install at /usr/local/gpdb
WORKDIR /gpdb_src
RUN ./configure --with-perl --with-python --with-libxml --with-gssapi --with-openssl --with-uuid --prefix=/usr/local/greenplum-db \
    && make -j8 \
    && make -j8 install

# RUN export DEBIAN_FRONTEND=noninteractive \
# && echo "/usr/local/lib" > /etc/ld.so.conf.d/usr-local.conf \
# && ldconfig \
# && ./README.Ubuntu.bash \
# && chmod +x concourse/scripts/setup_gpadmin_user.bash \
# && concourse/scripts/setup_gpadmin_user.bash
