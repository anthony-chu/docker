# Dockerfile Repository

This repository contains Docker images used for environment ceritification.
To build the respective docker images, navigate to their subdirectory and
execute the following:

```bash
docker build -t <tagname> .
```

## Docker images

Listed below are the currently available docker images:

- [Microsoft SQL Server 2017](/sql-server-2017)
- [Ubuntu 18.04](/ubuntu1804)
- [Microsoft Windows Server 2019](/win-server-2019)

<!--
TO DO

Reorganize directories:

/app-servers
/databases
    /sql-server-2017
/operating-systems
    /ubuntu-1804
    /win-server-2019
-->