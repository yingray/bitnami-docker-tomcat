FROM gcr.io/stacksmith-images/minideb:jessie-r11

MAINTAINER Bitnami <containers@bitnami.com>

ENV BITNAMI_IMAGE_VERSION=8.0.42-r0 \
    BITNAMI_APP_NAME=tomcat \
    PATH=/opt/bitnami/tomcat/bin:/opt/bitnami/java/bin:$PATH

# System packages required
RUN install_packages libc6 libxext6 libx11-6 libxcb1 libxau6 libxdmcp6 libglib2.0-0 libfreetype6 libfontconfig1 libstdc++6 libgcc1 zlib1g libselinux1 libpng12-0 libexpat1 libffi6 libpcre3 libxml2 liblzma5

# Additional modules required
RUN bitnami-pkg install java-1.8.0_121-0 --checksum 2743f753fd1ea88bf90352d95694f89ab0a0fb855cf0d1c7b2a6d92835f9ad27

# Install tomcat
RUN bitnami-pkg unpack tomcat-8.0.42-0 --checksum da6869296de3f34cd7d332062d748dd9ae040d89f993b9226d8bdfa335626913
RUN ln -sf /opt/bitnami/tomcat/data /app

COPY rootfs /

ENV TOMCAT_SHUTDOWN_PORT="8005" \
    TOMCAT_HTTP_PORT="8080" \
    TOMCAT_AJP_PORT="8009" \
    JAVA_OPTS="-Djava.awt.headless=true -XX:+UseG1GC -Dfile.encoding=UTF-8" \
    TOMCAT_USERNAME="user" \
    TOMCAT_ALLOW_REMOTE_MANAGEMENT="0"

VOLUME ["/bitnami/tomcat"]

EXPOSE 8080

ENTRYPOINT ["/app-entrypoint.sh"]

CMD ["nami", "start", "--foreground", "tomcat"]