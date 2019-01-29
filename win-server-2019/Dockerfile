## Requres at least Windows Server 2019 or
## Windows 10 build 17763 / Version 1809 to run
## Also requires use of Windows containers

FROM mcr.microsoft.com/windows/servercore:ltsc2019

ENV BASE_URL=https://releases.liferay.com/portal/snapshot-master/latest/ \
	7Z_FILE=liferay-portal-tomcat-master.7z

RUN cd c:\\Users\\Administrator\\Downloads

##
## TODO: Java installation
##
## Option 1: Figure out JDK8 installer download
## Option 2: Use JDK 11 installer
## Option 3: Have JDK8 installer alongside Dockerfile
##
## Silent installation instructions:
## https://www.java.com/en/download/help/silent_install.xml
##
## RUN set JAVA_HOME=c:\Program Files\Java\...
## RUN set PATH=%JAVA_HOME%;%JAVA_HOME%\bin;%PATH%
##

RUN powershell.exe -Command Invoke-WebRequest %BASE_URL%/%7Z_FILE% -O %7Z_FILE%

RUN powershell.exe -Command \
	Invoke-WebRequest https://www.7-zip.org/a/7z1806-x64.exe -O 7z1806-x64.exe

RUN 7z1806-x64.exe /S /D c:\\Program Files\\7-Zip

RUN set PATH=%PATH%;c:\\Program Files\\7-Zip

RUN cd c:\\Users\\Administrator\\Desktop

RUN 7z x ..\\%&Z_FILE% > NUL:

RUN cd liferay-portal-master

RUN echo setup.wizard.enabled=false >> portal-ext.properties && \
    echo browser.launcher.url= >> portal-ext.properties

RUN cd tomcat-9.0.10\\bin

CMD ["catalina.bat", "run"]