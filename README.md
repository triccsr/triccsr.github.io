works well on docker server.

```bash
docker run -it --rm --name hexo_container --mount type=bind,source=/home/triccsr/Documents/triccsr_blog_hexo,target=/app --workdir /app  --user "$(id -u):$(id -g)" hexo-next-mathjax-cn:v0 /bin/bash
```

In order to avoid permission errors.