# runq


## Redis
#### run redis with default configuration
```
docker run \
  -d \
  -p 6379:6379\
  -v <path/volume>:/data \
  --name redis \
  runq/redis:6.0.8
```

#### run redis with custom configuration
- create a Dockerfile
    ```
    FROM runq/redis:6.0.8
    COPY redis.conf /etc/redis/redis.conf
    ```
- build your docker imgae
    ```
    docker build -t <image_name> -f <path_to_Dockerfie> <context_folder>
    ```

## MinIO
```
docker run \
  -p 9000:9000 \
  -d \
  --name object_store \
  -v <path/volume>:/data \
  -e "MINIO_ACCESS_KEY=<your_key>" \
  -e "MINIO_SECRET_KEY=<your_secret>" \
  runq/minio server /data
```
