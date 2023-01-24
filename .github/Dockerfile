FROM ubuntu:18.04

COPY README.Ubuntu.bash /gpdb_src/README.Ubuntu.bash
COPY concourse/ /gpdb_src/concourse/

WORKDIR /gpdb_src

RUN export DEBIAN_FRONTEND=noninteractive \
&& echo "/usr/local/lib" > /etc/ld.so.conf.d/usr-local.conf \
&& ldconfig \
&& ./README.Ubuntu.bash \
&& chmod +x concourse/scripts/setup_gpadmin_user.bash \
&& concourse/scripts/setup_gpadmin_user.bash
