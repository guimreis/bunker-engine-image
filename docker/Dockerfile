ARG CAMUNDA_VERSION=7.24.0

FROM eclipse-temurin:17-jre-jammy

ARG CAMUNDA_VERSION
ENV CAMUNDA_HOME=/opt/bunker/app

RUN set -eux; \
    groupadd -r bunker || true; \
    useradd -r -g bunker -d /opt/bunker -s /usr/sbin/nologin bunker || true; \
    mkdir -p /opt/bunker/app; \
    chown -R bunker:bunker /opt/bunker

ADD distro/tomcat/distro/target/camunda-bpm-tomcat-${CAMUNDA_VERSION}.tar.gz /opt/bunker/app/

RUN set -eux; \
    ln -s /opt/bunker/app/server /opt/bunker/server; \
    chown -R bunker:bunker /opt/bunker/app

WORKDIR /opt/bunker/app/server
EXPOSE 8080
USER bunker
CMD ["/opt/bunker/app/server/bin/catalina.sh", "run"]
