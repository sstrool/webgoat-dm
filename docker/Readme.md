# Docker all-in-one image

## Docker build

```shell
docker build --no-cache --build-arg webgoat_version=8.2.0-SNAPSHOT -t webgoat/goatandwolf:latest .
```
	
## Docker run

```shell
docker run -p 127.0.0.1:80:8888 -p 127.0.0.1:8282:8282 -p 127.0.0.1:9292:9292 -e TZ=Europe/Amsterdam webgoat/goatandwolf:latest
```