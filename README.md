# Strimpack

*A tool for livestreamers to set up their own site, chat, subscription system, and forum.*

![how fancy](https://s3.amazonaws.com/bonner.jp/strimpack_large.png)

This is the central orchestration repo for the project. There are several other repositories containing the actual applications that are doing the work:

* [strimpack](https://github.com/j4p3/strimpack) webserver producing main website, handling authentication, payments, and client application prerendering
*  [strimchat](https://github.com/j4p3/strimchat) chatserver for client application
*  [strimpack web client](https://github.com/j4p3/strimpack-web-client) react app for main site

The application also uses other open source tools:

*  [discourse](https://github.com/discourse/discourse) forum application
*  redis
*  postgresql


## usage

**Can I configure this to match the way I want it to be?**

Sure. So far you can adjust the following items to suit you:

* title
* primary color
* logo
* subscription levels
* subscription prices
* stream location

And Discourse, the software powering the forum, has a whole slew of configuration options, too.

**Can I use this if I'm not a programmer?**

Sure. You'll need to be able to follow the steps below:

### setup instructions

1. Get a server. Not a tiny one.
2. Point a domain name at it. Then point `chat.<your domain>` and `forum.<your domain>` at it, too.
3. SSH into your server.
4. Install `docker`, `docker-compose`, and `git`.
5. `git clone https://github.com/j4p3/strimpack-container.git`
6. `cd strimpack-container`
7. Create an environment file to suit your application (default will read from `env.local` - details below)
8. `docker-compose up -d`
9. Wait a while. You should be able to visit the stream at `<your domain>` within a minute or two, but the forum will take several minutes to install.
10. You've got yourself a community website.

### items to note

The application has lots of external dependencies. In particular, you need:

* Email - valid credentials for sending email via SMTP
* Stripe - a Stripe account with some Subscription products in it
* Twitch - a Twitch account with an application registered on their developer console.

### environment variables

```
STREAM_TITLE
STREAM_CHANNEL
THEME_COLOR

TWITCH_CLIENT_ID
TWITCH_CLIENT_SECRET
TWITCH_CALLBACK_URI

STRIPE_PUBLISHABLE_KEY
STRIPE_SECRET_KEY

VIRTUAL_HOST
STRIMPACK_HOST
STRIMCHAT_HOST
FORUM_HOST

NODE_ENV

STRIMPACK_PORT
STRIMPACK_SESSION_SECRET

STRIMPACK_DB_USER
STRIMPACK_DB_PASSWORD
STRIMPACK_DB_NAME
STRIMPACK_DB_HOST
STRIMPACK_DB_PORT

STRIMCHAT_PORT

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

SMTP_HOST
SMTP_PORT
SMTP_USER
SMTP_PASSWORD

DISCOURSE_HOST
DISCOURSE_PORT
```

### help

Shoot me a message. This was a bit of a learning project, I'm happy to help you get something up and running. You can find me at [bonner.jp](https://bonner.jp).

### contributing

There are a million and one things to do here. Contributions are welcome.

*MIT license.*