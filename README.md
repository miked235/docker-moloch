# Moloch Docker Container

## Docker

For deploying a Moloch instance with Docker, please have a working Elasticsearch deployment running and a way to access it. You can edit the ```Dockerfile``` environment variables to set your configuration settings.  

The command below uses a Docker link to link the two containers together:

```
sysctl -w vm.max_map_count=262144
docker run -p 9200:9200 -p 9300:9300 --name elasticsearch docker.elastic.co/elasticsearch/elasticsearch:6.2.4
docker run -itd -p 8005:8005 --add-cap NET_RAW --add-cap NET_ADMIN --add-cap SYS_NICE --link elasticsearch:elasticsearch --name moloch moloch
```

## Kubernetes

For deploying multiple instances, it is recommended that you use a statefulset for both Elasticsearch and Moloch to prevent changes in the container/pod states. You may also want to use a config map for the ```config.ini``` file to further customize your deployment. 
