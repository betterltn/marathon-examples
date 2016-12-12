# marathon-examples
Here is a Sample marathon configuration for starting nginx webserver with three container instances in HA mode. 

1. Nginx cluster

{
"id": "/mywebserver",
"cmd": "nginx -g 'daemon off;'",
"cpus": 0.5,
"mem": 64,
"disk": 0,
"instances": 3,
"container": {
"type": "DOCKER",
"volumes": [],
"docker": {
"image": "nginx:stable",
"network": "BRIDGE",
"portMappings": [
{
"containerPort": 80,
"hostPort": 0,
"servicePort": 10004,
"protocol": "tcp",
"labels": {}
}
],
"privileged": false,
"parameters": [],
"forcePullImage": false
}
},
"healthChecks": [
{
"path": "/",
"protocol": "HTTP",
"portIndex": 0,
"gracePeriodSeconds": 5,
"intervalSeconds": 20,
"timeoutSeconds": 20,
"maxConsecutiveFailures": 3,
"ignoreHttp1xx": false
}
],
"labels": {
"HAPROXY_GROUP": "external"
},
"portDefinitions": [
{
"port": 10004,
"protocol": "tcp",
"labels": {}
}
]
}





You can see more examples at http://www.techietown.info/2016/12/marathon-lb-service-discovery-and-loadbalancing-for-containers-running-on-mesosmarathon/
