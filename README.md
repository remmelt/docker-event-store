#Docker Event Store image

A Docker image with the [Event Store](http://geteventstore.com/). Based on debian:sid, this image is about 850MB.

##Usage
```
docker run -dP remmelt/docker-event-store:latest
```

Any command line arguments can be passed with the `docker run` command (e.g. `docker run -dP remmelt/docker-event-store:latest --use-internal-ssl=true`) or set in an environment variable (`docker run -dP -e "EVENTSTORE_USE_INTERNAL_SSL=true" remmelt/docker-event-store:latest`)

See [the Eventstore documentation](http://docs.geteventstore.com/introduction/command-line-arguments/) for possible arguments.

##Volumes

There are two volumes: /db and /logs. Pass them to `docker run` with `-v`.


##Issues

###Webpage not available
Visiting `http://x.x.x.x:PORT/` results in a redirect to `http://x.x.x.x:2113/web/index.html` and a 404 or "Webpage not available" message.

This is because the redirect checks the external port and assumes it runs on that port.

Fix this by visiting `http://x.x.x.x:PORT/web/index.html` directly.
