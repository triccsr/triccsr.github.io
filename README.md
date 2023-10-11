Works well on docker.

For users in China mainland, build a docker image with Dockerfile:

```dockerfile
FROM node:18.18.0
ENV LC_ALL=C.utf8 TZ="Asia/Shanghai" #enable Chinese language support and set timezone to Shanghai
RUN date\ 
&& npm install -g npm@latest\
&& npm install -g hexo-cli
```
Then run a container with commands:

```bash
docker run -it --rm --name hexo_container \
--mount type=bind,source=YOUR_PATH_OF_PAGES_DIRECTORY,target=/app \
--workdir /app \
--user "$(id -u):$(id -g)" \
YOUR_DOCKER_IMAGE_NAME \
/bin/bash
```


The `--user` option is set to `"$(id -u):$(id -g)"` in order to avoid permission issues. Otherwise, files created within the Docker container will not be modifiable outside the Docker container.