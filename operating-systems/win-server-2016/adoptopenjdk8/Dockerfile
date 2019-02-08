## Requres at least Windows Server 2016 or
## Windows 10 build 17763 / Version 1709 to run
## Also requires use of Windows containers

## NOTE:
## Please provide at least 2GB of memory in order to build this image and
## run this container

FROM mcr.microsoft.com/windows/servercore:ltsc2016

ENV 7Z_INSTALL_DIR=C:\\Program\ Files\\7-Zip \
	7Z_INSTALL_FILE=7z1806-x64.exe \
	ADOPT_JDK_URL=https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u202-b08 \
	ADOPT_JDK_ZIP=OpenJDK8U-jdk_x64_windows_hotspot_8u202b08.zip \
	JAVA_DIR=C:\\Program\ Files\\Java \
	SNAPSHOT_FILE=liferay-portal-tomcat-master.7z \
	SNAPSHOT_URL=https://releases.liferay.com/portal/snapshot-master/latest

# Download snapshot-master, 7-Zip, and AdoptOpenJDK; install 7-Zip

RUN cd %USERPROFILE%\\Downloads && \
	powershell.exe -Command $ProgressPreference = 'SilentlyContinue'; \
		Invoke-WebRequest %SNAPSHOT_URL%/%SNAPSHOT_FILE% -O %SNAPSHOT_FILE% && \
	powershell.exe -Command \
		$ProgressPreference = 'SilentlyContinue'; \
		Invoke-WebRequest https://www.7-zip.org/a/%7Z_INSTALL_FILE% -O %7Z_INSTALL_FILE% && \
	powershell.exe [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; \
		$ProgressPreference = 'SilentlyContinue'; \
		Invoke-WebRequest %ADOPT_JDK_URL%/%ADOPT_JDK_ZIP% -O %ADOPT_JDK_ZIP% && \
	%7Z_INSTALL_FILE% /S /D %7Z_INSTALL_DIR% && \
	setx PATH "%PATH%;%7Z_INSTALL_DIR%"

# Install AdoptOpenJDK-8

RUN	cd %PROGRAMFILES% && \
	mkdir Java && \
	cd %JAVA_DIR% && \
	7z x %USERPROFILE%\\Downloads\\%ADOPT_JDK_ZIP% > NUL: && \
	setx JAVA_HOME "%PROGRAMFILES%\\Java\\jdk8u202-b08" && \
	setx PATH "%JAVA_HOME%;%JAVA_HOME%\\bin;%PATH%"

RUN cd %USERPROFILE%\\Desktop && \
	7z x ..\\Downloads\\%SNAPSHOT_FILE% > NUL: && \
	cd liferay-portal-master && \
	echo setup.wizard.enabled=false >> portal-ext.properties && \
    echo browser.launcher.url= >> portal-ext.properties

COPY init.bat c:\\init.bat

CMD [ "c:\\init.bat" ]

EXPOSE 8080