## Requres at least Windows Server 2019 or
## Windows 10 build 17763 / Version 1809 to run
## Also requires use of Windows containers

FROM mcr.microsoft.com/windows/servercore:ltsc2019

ENV 7Z_INSTALL_DIR=%PROGRAMFILES%\\7-Zip \
	7Z_INSTALL_FILE=7z1806-x64.exe \
	ADOPT_JDK_URL=https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u202-b08 \
	ADOPT_JDK_ZIP=OpenJDK8U-jdk_x64_windows_hotspot_8u202b08.zip \
	JAVA_DIR=%PROGRAMFILES%\\Java \
	SNAPSHOT_FILE=liferay-portal-tomcat-master.7z \
	SNAPSHOT_URL=https://releases.liferay.com/portal/snapshot-master/latest

RUN SETLOCAL ENABLEEXTENSIONS && \
	cd c:\\Users\\Administrator\\Downloads && \
	powershell.exe -Command $ProgressPreference = 'SilentlyContinue'; \
		Invoke-WebRequest %SNAPSHOT_URL%/%SNAPSHOT_FILE% -O %SNAPSHOT_FILE% && \
	powershell.exe -Command \
		$ProgressPreference = 'SilentlyContinue'; \
		Invoke-WebRequest https://www.7-zip.org/a/%7Z_INSTALL_FILE% -O %7Z_INSTALL_FILE% && \
	%7Z_INSTALL_FILE% /S /D %7Z_INSTALL_DIR% && \
	set PATH=%PATH%;%7Z_INSTALL_DIR% && \
	powershell.exe -Command \
		$ProgressPreference = 'SilentlyContinue'; \
		Invoke-WebRequest %ADOPT_JDK_URL%/%ADOPT_JDK_ZIP% -O %ADOPT_JDK_ZIP% && \
	cd "%PROGRAMFILES%" && \
	md Java && \
	cd "%JAVA_DIR%" %% \
	7z x c:\\Users\\Administrator\\Downloads\\%ADOPT_JDK_ZIP% > NUL: && \
	set JAVA_HOME=%JAVA_DIR%\jdk8u202-b08 && \
	set PATH=%JAVA_HOME%;%JAVA_HOME%\bin;%PATH% && \
	cd c:\\Users\\Administrator\\Desktop && \
	7z x ..\\%SNAPSHOT_FILE% > NUL: && \
	del c:\\Users\Administrator\\Downloads\* && \
	cd liferay-portal-master && \
	echo setup.wizard.enabled=false >> portal-ext.properties && \
    echo browser.launcher.url= >> portal-ext.properties

CMD ["c:\\Users\\Administrator\\Desktop\\tomcat-9.0.10\\bin\\catalina.bat", "run"]