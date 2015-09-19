# Containers! Containers! Containers! And Now?

Containers are all the hype, and rightly so. But what do you do after you've build your Docker images? Are you going all-in concerning microservices? What about existing workloads you can't or don't want to containerize? We will discuss options and tooling to address these and related questions.

## Preparation

In order to recreate the experience you will have to ramp up a [DCOS cluster](https://mesosphere.com/product/), using 3 private worker nodes and 1 public node. Install the DCOS CLI here (the directory where you did `git clone` this repo). Further, here are two things you need to prepare for the first part:

- ssh onto the Master, vim google-search.py and paste content
- mkdir snowflake && touch index.html and paste content from snowflake/index.html

## Talk

    ] Intro
    ssh -A core@IP_ADDRESS_OF_MASTER
    alias cowsay='docker run schu/cowsay'
    cat /etc/os-release
    cowsay "Containers! Containers! Containers! And Now?"
    alias
    docker images
    docker run -it --rm -v "$PWD":/usr/src/myapp -w /usr/src/myapp python:2 python google-search.py "software eats the world"
    cowsay "... and containers eat the software."
    docker run -v /home/core/snowflake:/usr/share/nginx/html:ro -p 8888:80 nginx:latest
    http://IP_ADDRESS_OF_MASTER:8888/
    cowsay "pets vs cattle"
    exit
    
    ] Now what?
    Approach 1: manually maintaining the app <-> server:port mapping (hello pager duty :)
    Approach 2: container cluster manager: Enter Marathon!
    dcos marathon app add marathon-webserver.json
    dcos marathon app show webserver | grep -w tasks -A 8
    http://DNS_NAME_OF_PUBLIC_SLAVE:
    SCALE: 5
    
    ] Failure! Failure! Failure!
    ssh -A core@IP_ADDRESS_OF_MASTER
    ssh IP_ADDRESS_OF_PUBLIC_NODE
    docker kill 
    exit
    exit
    
    ] Let's deploy an end-to-end application:
    https://mesosphere.com/blog/2015/06/21/web-application-analytics-using-docker-and-marathon/
    dcos marathon group add m-shop.json
    
    ] Selected good practises:
    GP1: monitor all the thingz
    dcos marathon app add marathon-cadvisor.json
    GP2: use a private registry
    dcos marathon app add marathon-private-registry.json
    GP3: service discovery options
    http://p24e.io and if that is not available, see:
    https://github.com/programmableinfrastructure/p24e.io
    
    ] Q & A
    dcos marathon app add marathon-q-and-a.json
