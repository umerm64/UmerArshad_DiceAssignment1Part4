# UmerArshad_DiceAssignment1Part4
Docker Networking

# Step 1
`docker network create my_network`

# Step 2
`docker run --network my_network --name nginx_container -p 8080:80 nginx`

# Step 3
nginx welcome page is visible.

# Step 4
`docker run --network my_network --name httpd_container -p 8081:80 httpd`

# Step 5
httpd default page is visible.

# Step 6
`docker network inspect my_network`
```
[
    {
        "Name": "my_network",
        "Id": "fd8be1f756220b0f62b1c1edd115a29f02da15078677d1f3ab8b3b966ee765c7",
        "Created": "2023-03-23T20:58:19.667385113+05:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.25.0.0/16",
                    "Gateway": "172.25.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "e6e0ffa8f743e1a12664df7a3e092b50b9b6a033e3a6dd703a0abf65e9c4d15c": {
                "Name": "httpd_container",
                "EndpointID": "e97ae46f413044f664118318645ac1bdb71bbc3b079f7421eb22091230fb511e",
                "MacAddress": "02:42:ac:19:00:03",
                "IPv4Address": "172.25.0.3/16",
                "IPv6Address": ""
            },
            "ea8e3516671e7f405f5c808bd7cc082852ae7ae5b6a943810d961b54e8246bdb": {
                "Name": "nginx_container",
                "EndpointID": "ce1c8eeb813af849ceef3d4969a120f92b726291e97c21e4bd8ff3fd87898500",
                "MacAddress": "02:42:ac:19:00:02",
                "IPv4Address": "172.25.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]
```

# Step 7
`docker stop nginx_container`
`docker rm nginx_container`

# Step 8
`docker run --network my_network --name nginx_container_2 -p 8082:80 nginx`

# Step 9
The nginx welcome page is visible.

# Step 10
`docker container ls`
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                       NAMES
4dcd246ea690   nginx     "/docker-entrypoint.…"   55 seconds ago   Up 54 seconds   0.0.0.0:8082->80/tcp, :::8082->80/tcp       nginx_container_2
e6e0ffa8f743   httpd     "httpd-foreground"       3 minutes ago    Up 3 minutes    0.0.0.0:8081->80/tcp, :::8081->80/tcp       httpd_container
d12e02d5be95   task1     "python app.py"          52 minutes ago   Up 40 minutes   0.0.0.0:5000->5000/tcp, :::5000->5000/tcp   task2

# Step 11
`docker stop $(docker ps -aq)`
`docker rm $(docker ps -aq)`

# Step 12
`docker network rm my_network`
