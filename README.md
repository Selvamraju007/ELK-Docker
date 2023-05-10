# docker-elk
ELK stack in Docker

$ git clone https://github.com/Selvamraju007/Docker-ELK.git

$ cd docker-elk

$ docker-compose up -d

Elasticsearch is the first resource to be set up. A mechanism for swiftly analysing and analysing various forms of data is called elasticsearch. Using environment variables, we may use a single instance and turn off xpack (a paid feature). It is set up on the Docker bridge network called the logging-network.

    elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.1.1
    environment:   
    - discovery.type=single-node
    - xpack.security.enabled=false    
    networks: 
    - logging-network
    
We will now set up Logstash. An open source server-side data processing pipeline called Logstash ingests data from numerous sources at once, alters it, and then forwards it to applications like Elasticsearch.
    
    logstash:
    image: docker.elastic.co/logstash/logstash:7.1.1
    depends_on:
    - elasticsearch
    ports:
    - 12201:12201/udp
    volumes:
    - ./logstash.conf:/usr/share/logstash/pipeline/logstash.conf:ro
    networks:
    - logging-network
    
    
