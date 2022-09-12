FROM alpine:3.15

ARG JMETER_VERSION="5.4.3"

ENV JMETER_HOME /opt/apache-jmeter-${JMETER_VERSION}
ENV JMETER_BIN  ${JMETER_HOME}/bin
ENV MIRROR_HOST http://mirrors.ocf.berkeley.edu/apache/jmeter
ENV JMETER_DOWNLOAD_URL ${MIRROR_HOST}/binaries/apache-jmeter-${JMETER_VERSION}.tgz
ENV JMETER_PLUGINS_DOWNLOAD_URL https://repo1.maven.org/maven2
ENV JMETER_PLUGINS_FOLDER ${JMETER_HOME}/lib/ext/

RUN    apk update \
	&& apk upgrade \
	&& apk add ca-certificates \
	&& update-ca-certificates \
            && apk add --update openjdk8-jre tzdata curl unzip bash \
            && cp /usr/share/zoneinfo/Europe/Rome /etc/localtime \
            && echo "Europe/Rome" >  /etc/timezone \
	&& rm -rf /var/cache/apk/* \
	&& mkdir -p /tmp/dependencies  \
	&& curl -L --silent ${JMETER_DOWNLOAD_URL} >  /tmp/dependencies/apache-jmeter-${JMETER_VERSION}.tgz  \
	&& mkdir -p /opt  \
	&& tar -xzf /tmp/dependencies/apache-jmeter-${JMETER_VERSION}.tgz -C /opt  \
	&& rm -rf /tmp/dependencies

RUN curl -L --silent ${JMETER_PLUGINS_DOWNLOAD_URL}/kg/apc/jmeter-plugins-dummy/0.2/jmeter-plugins-dummy-0.2.jar -o ${JMETER_PLUGINS_FOLDER}/jmeter-plugins-dummy-0.2.jar
RUN curl -L --silent ${JMETER_PLUGINS_DOWNLOAD_URL}/kg/apc/jmeter-plugins-cmn-jmeter/0.5/jmeter-plugins-cmn-jmeter-0.5.jar -o ${JMETER_PLUGINS_FOLDER}/jmeter-plugins-cmn-jmeter-0.5.jar
RUN curl -L --silent ${JMETER_PLUGINS_DOWNLOAD_URL}/kg/apc/jmeter-plugins-casutg/2.10/jmeter-plugins-casutg-2.10.jar -o ${JMETER_PLUGINS_FOLDER}/jmeter-plugins-casutg-2.10.jar
RUN curl -L --silent ${JMETER_PLUGINS_DOWNLOAD_URL}/cloud/testload/jmeter.pack-listener/1.7/jmeter.pack-listener-1.7.jar -o ${JMETER_PLUGINS_FOLDER}/jmeter.pack-listener-1.7.jar


ENV PATH $PATH:$JMETER_BIN

COPY launch.sh /

WORKDIR ${JMETER_HOME}

ENTRYPOINT ["/launch.sh"]