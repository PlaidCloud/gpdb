FROM ubuntu:18.04

COPY greenplum-oss/sysconf.bash /gpdb_src/sysconf.bash
COPY concourse/ /gpdb_src/concourse/

WORKDIR /gpdb_src

RUN echo "/usr/local/lib" > /etc/ld.so.conf.d/usr-local.conf \
&& ldconfig

RUN export DEBIAN_FRONTEND=noninteractive \
&& chmod +x sysconf.bash \
&& ./sysconf.bash

RUN chmod +x concourse/scripts/setup_gpadmin_user.bash \
&& concourse/scripts/setup_gpadmin_user.bash

# RUN export DEBIAN_FRONTEND=noninteractive \
# && echo "/usr/local/lib" > /etc/ld.so.conf.d/usr-local.conf \
# && ldconfig \
# && ./README.Ubuntu.bash \
# && chmod +x concourse/scripts/setup_gpadmin_user.bash \
# && concourse/scripts/setup_gpadmin_user.bash
