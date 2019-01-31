FROM ubuntu:18.04

ENV BASE_URL=https://releases.liferay.com/portal/snapshot-master/latest/
ENV ARCHIVE_FILE=liferay-portal-tomcat-master.7z
ENV LIFERAY_HOME=liferay-portal-master

RUN apt-get update && \
    apt-get install -y openjdk-8-jdk p7zip-full wget && \
    cd /home/ && \
    wget ${BASE_URL}/${ARCHIVE_FILE} && \
    7z x ${ARCHIVE_FILE} && \
    cd ${LIFERAY_HOME} && \
    echo "browser.launcher.url=" >> portal-ext.properties && \
    echo "setup.wizard.enabled=false" >> portal-ext.properties

COPY entrypoint.sh /entrypoint.sh

CMD [ "./entrypoint.sh" ]

EXPOSE 8080