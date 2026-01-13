ARG CAMUNDA_VERSION=7.24.0

FROM eclipse-temurin:17-jre-jammy

ARG CAMUNDA_VERSION
ENV CAMUNDA_HOME=/opt/bunker/app/tomcat

RUN set -eux; \
    groupadd -r bunker || true; \
    useradd -r -g bunker -d /opt/bunker -s /usr/sbin/nologin bunker || true; \
    mkdir -p /opt/bunker/app; \
    chown -R bunker:bunker /opt/bunker

ADD distro/tomcat/distro/target/camunda-bpm-tomcat-${CAMUNDA_VERSION}.tar.gz /opt/bunker/app/

RUN set -eux; \
    TOMCAT_DIR="$(ls -d /opt/bunker/app/server/apache-tomcat-* | head -n 1)"; \
    ln -s "${TOMCAT_DIR}" /opt/bunker/app/tomcat; \
    ln -s /opt/bunker/app/tomcat /opt/bunker/server; \
    chown -R bunker:bunker /opt/bunker/app

WORKDIR /opt/bunker/app/tomcat
EXPOSE 8080
USER bunker
CMD ["/opt/bunker/app/tomcat/bin/catalina.sh", "run"]
