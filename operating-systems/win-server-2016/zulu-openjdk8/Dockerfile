## Requres at least Windows Server 2016 or Windows 10 build 16299 / Version 1709
## to run; also requires use of Windows containers

## NOTE:
## Please provide at least 2GB of memory in order to build this image and
## run this container

FROM mcr.microsoft.com/java/jdk:8u202-zulu-windowsservercore

ENV 7Z_INSTALL_DIR=C:\\Program\ Files\\7-Zip \
	7Z_INSTALL_FILE=7z1806-x64.exe \
	SNAPSHOT_FILE=liferay-portal-tomcat-master.7z \
	SNAPSHOT_URL=https://releases.liferay.com/portal/snapshot-master/latest

# Download snapshot-master and 7-Zip; install 7-Zip

RUN cd %USERPROFILE%\\Downloads && \
	powershell.exe -Command $ProgressPreference = 'SilentlyContinue'; \
		Invoke-WebRequest %SNAPSHOT_URL%/%SNAPSHOT_FILE% -O %SNAPSHOT_FILE% && \
	powershell.exe -Command \
		$ProgressPreference = 'SilentlyContinue'; \
		Invoke-WebRequest https://www.7-zip.org/a/%7Z_INSTALL_FILE% -O %7Z_INSTALL_FILE% && \
	%7Z_INSTALL_FILE% /S /D %7Z_INSTALL_DIR% && \
	setx PATH "%PATH%;%7Z_INSTALL_DIR%"

RUN cd %USERPROFILE%\\Desktop && \
	7z x ..\\Downloads\\%SNAPSHOT_FILE% > NUL: && \
	cd liferay-portal-master && \
	echo setup.wizard.enabled=false >> portal-ext.properties && \
    echo browser.launcher.url= >> portal-ext.properties

COPY init.bat c:\\init.bat

CMD [ "c:\\init.bat" ]

EXPOSE 8080