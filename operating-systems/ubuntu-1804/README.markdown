# Ubuntu 18.04

## Environment Details

|Product|Version|
|:-----:|:-----:|
|Java|OpenJDK JDK 8|
|Portal| master snapshot|

## Startup

```bash
docker build -t <tag> .

docker run -p 8080:8080 -d <tag>:latest
```

This will start up a Liferay instance on Tomcat using HSQLDB.