FROM ubuntu:18.04

ARG NSOVER

COPY nso-$NSOVER.linux.x86_64.installer.bin /tmp/nso
RUN apt-get update; \
    apt-get install -y openssh-client; \
    /tmp/nso --system-install; \
    rm -rf /opt/ncs/current/var/ncs/webui; \
    rm -rf /opt/ncs/current/doc; \
    rm -rf /opt/ncs/current/man; \
    rm -rf /opt/ncs/current/examples.ncs; \
    rm -rf /opt/ncs/current/include; \
    rm -rf /opt/ncs/current/packages; \
    rm -rf /opt/ncs/current/support; \
    rm -rf /opt/ncs/current/src/aaa; \
    rm -rf /opt/ncs/current/src/build; \
    rm -rf /opt/ncs/current/src/cli; \
    rm -rf /opt/ncs/current/src/configuration_policy; \
    rm -rf /opt/ncs/current/src/errors; \
    rm -rf /opt/ncs/current/src/ncs_config; \
    rm -rf /opt/ncs/current/src/netconf; \
    rm -rf /opt/ncs/current/src/package-skeletons; \
    rm -rf /opt/ncs/current/src/project-skeletons; \
    rm -rf /opt/ncs/current/src/snmp; \
    rm -rf /opt/ncs/current/src/tools; \
    rm -rf /opt/ncs/current/src/yang; \
    rm -rf /opt/ncs/current/lib/ncs/lib/confdc; \
    rm -rf /opt/ncs/current/lib/ncs-project; \
    rm -rf /opt/ncs/current/lib/pyang; \
    rm -rf /opt/ncs/current/erlang

FROM ubuntu:18.04

RUN apt-get update; \
    apt-get install -y openssh-client default-jre-headless python; \
    echo '. /opt/ncs/current/ncsrc' >> /root/.bashrc; \
    apt-get -y clean autoclean; \
    apt-get -y autoremove; \
    rm -rf /tmp/* /var/tmp/* /var/lib/{apt,dpkg,cache,log}/; \
    mkdir /var/log/ncs;

COPY --from=0 /etc/ncs /etc/ncs/
COPY --from=0 /var/opt/ncs /var/opt/ncs/
COPY --from=0 /opt/ncs /opt/ncs/
COPY --from=0 /etc/init.d/ncs /etc/init.d/.

COPY run-nso.sh /
COPY admin.xml /var/opt/ncs/cdb/

EXPOSE 8080 830 2022 2023 4569

CMD ["/run-nso.sh"]