FROM ubuntu:16.04

ENV ACCEPT_EULA="Y"
ENV MSSQL_SA_PASSWORD="Password1"
ENV MSSQL_PID="Developer"

RUN apt-get update && \
    apt-get install -y wget curl software-properties-common apt-transport-https && \
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)" && \
    apt-get update && \
    apt-get install -y mssql-server && \
    /opt/mssql/bin/mssql-conf -n setup

CMD [ "/opt/mssql/bin/sqlservr" ]

EXPOSE 1433