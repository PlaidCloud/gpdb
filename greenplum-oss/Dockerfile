FROM ubuntu:18.04

COPY ./ /gpdb_src/
# COPY greenplum-oss/sysconf.bash /gpdb_src/sysconf.bash
# COPY concourse/ /gpdb_src/concourse/

WORKDIR /
ENV DEBIAN_FRONTEND=noninteractive

RUN echo "/usr/local/lib" > /etc/ld.so.conf.d/usr-local.conf \
&& ldconfig

RUN chmod +x gpdb_src/greenplum-oss/sysconf.bash \
&& gpdb_src/greenplum-oss/sysconf.bash

RUN chmod +x gpdb_src/concourse/scripts/setup_gpadmin_user.bash \
&& gpdb_src/concourse/scripts/setup_gpadmin_user.bash

WORKDIR /gpdb_src

# RUN python -v

# Configure build environment to install at /usr/local/gpdb
RUN ./configure --with-perl --with-python --with-libxml --with-gssapi --prefix=/usr/local/gpdb
RUN make -j8
RUN make -j8 install

# RUN export DEBIAN_FRONTEND=noninteractive \
# && echo "/usr/local/lib" > /etc/ld.so.conf.d/usr-local.conf \
# && ldconfig \
# && ./README.Ubuntu.bash \
# && chmod +x concourse/scripts/setup_gpadmin_user.bash \
# && concourse/scripts/setup_gpadmin_user.bash
