# Strimpack Container

*Orchestration for strimpack applications.*

Docker Compose file for running strimpack system on one server.

## usage:
In a server with `docker` and `docker-compose` installed:
```
git clone git@github.com:j4p3/strimpack-container.git
cd strimpack-container
docker-compose up
```

This will start services for:

* [strimpack](https://github.com/j4p3/strimpack) webserver producing main website, handling authentication, payments, and client application prerendering
*  [strimchat](https://github.com/j4p3/strimchat) chatserver for client application
*  [strimpack web client](https://github.com/j4p3/strimpack-web-client) react app for main site
*  [discourse](https://github.com/discourse/discourse) forum application
*  redis
*  postgresql

Then to complete the installation, some manual steps:

1. expose ports on your server
2. configure DNS
3. set up discourse installation
