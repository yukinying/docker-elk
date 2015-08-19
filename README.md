Elasticsearch. Logstash. Kibana.
================================

Source [Github](https://github.com/yukinying/docker-elk)

The intention of this repository from cloning https://github.com/willdurand/docker-elk are

1. exposing 5000 as tcp with json_line codec
2. use of latest ELK 


// The following instruction are extracted and modified from https://github.com/willdurand/docker-elk 

Creating an ELK stack could not be easier.

**Important:** this image embeds Kibana 4.1.0.

Quick Start
-----------

```
$ docker run -p 8080:5601 yukinying/elk
    
# OR 
$ docker run -p 8080:5601 \
    -v /path/to/your/logstash/config:/etc/logstash \
    yukinying/elk
```

Then, browse: [http://localhost:8080](http://localhost:8080) (replace
`localhost` with your public IP address).

Your logstash configuration directory MUST contain at least one logstash configuration file. If several files are found in the configuration directory, logstash will use all of them, concatenated in lexicographical order, as the configuration.



Data
----

Elasticsearch data are located in the `/data` folder. It is probably a good idea
to mount a volume in order to preserve data integrity. You can create a _data
only container_:

```
$ docker run -d -v /data --name dataelk busybox
```

Then, use it:

```
$ docker run -p 8080:5601 \
    --volumes-from dataelk \
    yukinying/elk
```


