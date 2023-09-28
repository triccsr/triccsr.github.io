works well on docker server.

```bash
docker run -it --rm --name hexo_c --mount type=bind,source=/home/triccsr/Documents/triccsr_blog_permission,target=/app --workdir /app  --user "$(id -u):$(id -g)" hexo-next-mathjax-cn/bin/bash
```

In order to avoid permission errors.