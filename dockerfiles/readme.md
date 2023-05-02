## Create Docker Image

```shell
cd dockerfiles
docker build .
docker images
docker tag <ID> <User>/<Image>:<Ver>
docker push <User>/<Image>:<Ver>
```

To add additional models, copy the format of line 82 in the Dockerfile
```shell
ADD https://civitai.com/api/download/models/<Model ID> ./models/Stable-diffusion/<Model Name>
```