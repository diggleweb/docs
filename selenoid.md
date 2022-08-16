# install selenoid


```shell
docker run -d                                   \
--name selenoid                                 \
-p 4444:4444                                    \
-v /var/run/docker.sock:/var/run/docker.sock    \
-v /Users/alexyucra/.aerokube/selenoid:/etc/selenoid/:ro \
aerokube/selenoid:latest-release
```