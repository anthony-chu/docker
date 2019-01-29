## Requres at least Windows Server 2019 or
## Windows 10 build 17763 / Version 1809 to run
## Also requires use of Windows containers

FROM mcr.microsoft.com/windows/servercore:ltsc2019

ENV ADOPT_JDK_URL=https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u202-b08 \
	ADOPT_JDK_ZIP=OpenJDK8U-jdk_x64_windows_hotspot_8u202b08.zip \
	JAVA_DIR="c:\\Program Files\\Java" \
	SNAPSHOT_FILE=liferay-portal-tomcat-master.7z \
	SNAPSHOT_URL=https://releases.liferay.com/portal/snapshot-master/latest/

RUN cd c:\\Users\\Administrator\\Downloads

RUN powershell.exe -Command Invoke-WebRequest %SNAPSHOT_URL%/%SNAPSHOT_FILE% -O %SNAPSHOT_FILE%

RUN powershell.exe -Command \
	Invoke-WebRequest https://www.7-zip.org/a/7z1806-x64.exe -O 7z1806-x64.exe

RUN 7z1806-x64.exe /S /D c:\\Program Files\\7-Zip

RUN set PATH=%PATH%;c:\\Program Files\\7-Zip

RUN powershell.exe -Command Invoke-WebRequest %ADOPT_JDK_URL%/%ADOPT_JDK_ZIP% -O %ADOPT_JDK_ZIP%

RUN md %JAVA_DIR%

RUN cd %JAVA_DIR%

RUN 7z x c:\\Users\\Administrator\\Downloads\\%ADOPT_JDK_ZIP% > NUL:

RUN set JAVA_HOME=%JAVA_DIR%\jdk8u202-b08

RUN set PATH=%JAVA_HOME%;%JAVA_HOME%\bin;%PATH%

RUN cd c:\\Users\\Administrator\\Desktop

RUN 7z x ..\\%SNAPSHOT_FILE% > NUL:

RUN cd liferay-portal-master

RUN echo setup.wizard.enabled=false >> portal-ext.properties && \
    echo browser.launcher.url= >> portal-ext.properties

RUN cd tomcat-9.0.10\\bin

CMD ["catalina.bat", "run"]