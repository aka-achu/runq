# docker.pkg.github.com/aka-achu/docker/* 


#### You need to authenticate for the docker.pkg.github.com image registry
`
cat ~/GH_TOKEN.txt | docker login docker.pkg.github.com -u <user_name>" --password-stdin
`

## Redis
#### run redis with default configuration
```
docker run -d -p 6379:6379 -v <path/volume>:/data --name redis docker.pkg.github.com/aka-achu/docker/redis:6.0.6
```

#### run redis with custom configuration
- create a Dockerfile
    ```
    FROM docker.pkg.github.com/aka-achu/docker/redis:6.0.6
    COPY redis.conf /etc/redis/redis.conf
    ```
- build your docker imgae
    ```
    docker build -t <image_name> -f <path_to_Dockerfie> <context_folder>
    ```

## MinIO
```
docker run -d -p 9000:9000 --name object_store -e "MINIO_ACCESS_KEY=<your_key>" -e "MINIO_SECRET_KEY=<your_secret>" -v <path/volume>:/data minio/minio server /data
```
