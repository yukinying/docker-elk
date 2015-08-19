Elasticsearch. Logstash. Kibana.
================================

Source [Github](https://github.com/yukinying/docker-elk)

This is a clone from https://github.com/willdurand/docker-elk, with the following modifications:

1. exposing 5000 as tcp with json_line codec
2. use of latest ELK 


## Quick Start

(Based on https://github.com/willdurand/docker-elk with modification)

### Ports:
1. 5601: Kibana
2. 5000: Logstash, TCP, JSON_LINE

### Run 
```
$ docker run --name elk -p 8080:5601 -p 5000:5000 yukinying/elk
    
# OR with your own configs
$ docker run --name elk -p 8080:5601 -p 5000:5000
    -v /path/to/your/logstash/config:/etc/logstash \
    yukinying/elk
```

Then, browse: [http://localhost:8080](http://localhost:8080) 

## Persistent Storage (mount /data)

1. Create your own volume container.
```
$ docker run -d -v /data --name dataelk busybox
```

2. Link the containers.
```
$ docker run --name elk -p 8080:5601 -p 5000:5000\
    --volumes-from dataelk \
    yukinying/elk
```

## Troubleshooting 

Logs are stored in 

- `/var/log/supervisor/`
- `/var/log/logstash/`
- `/var/log/elasticsearch/`

To get the logs, run:
```
$ docker exec -it elk "/bin/bash"
$ tail -f /var/log/supervisor/* /var/log/logstash/* /var/log/elasticsearch/*
```


