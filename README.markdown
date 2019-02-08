# Dockerfile Repository

This repository contains Docker images used for environment ceritification.
To build the respective docker images, navigate to their subdirectory and
execute the following:

```bash
docker build -t <tagname> .
```

## Docker images

Listed below are the currently available docker images:

- [Ubuntu 18.04](/operating-systems/ubuntu1804)
- [Microsoft Windows Server 2016]
    - [With AdoptOpenJDK8](/operating-systems/win-server-2016/adoptopenjdk8)
    - [With Azul Zulu JDK 8](/operating-systems/win-server-2016/zulu-openjdk8)
- [Microsoft Windows Server 2019](/operating-systems/win-server-2019)