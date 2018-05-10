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

### environment variables

```
NODE_ENV

TWITCH_CLIENT_ID
TWITCH_CLIENT_SECRET
TWITCH_CALLBACK_URI

STRIPE_PUBLISHABLE_KEY
STRIPE_SECRET_KEY

STRIMPACK_SERVER_HOST
STRIMPACK_SERVER_PORT
STRIMPACK_SESSION_SECRET
STRIMPACK_DB_USER
STRIMPACK_DB_PASSWORD
STRIMPACK_DB_NAME
STRIMPACK_DB_HOST
STRIMPACK_DB_PORT

POSTGRESQL_PASSWORD

DISCOURSE_USERNAME
DISCOURSE_PASSWORD
DISCOURSE_EMAIL
DISCOURSE_SITENAME
POSTGRESQL_HOST
POSTGRESQL_PORT_NUMBER
POSTGRESQL_ROOT_USER
POSTGRESQL_ROOT_PASSWORD
POSTGRESQL_CLIENT_CREATE_DATABASE_NAME
POSTGRESQL_CLIENT_CREATE_DATABASE_USERNAME
POSTGRESQL_CLIENT_CREATE_DATABASE_PASSWORD
DISCOURSE_POSTGRESQL_USERNAME
DISCOURSE_POSTGRESQL_PASSWORD
DISCOURSE_POSTGRESQL_NAME

REDIS_PASSWORD

DISCOURSE_HOST
DISCOURSE_PORT
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
