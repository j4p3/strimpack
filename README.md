# Strimpack

*A tool for livestreamers to set up their own site, chat, subscription system, and forum.*

![how fancy](https://s3.amazonaws.com/bonner.jp/strimpack_large.png)

## [live demo](http://strimpack.unqualified.io/)

This is the central orchestration repo for the project. The applications that are doing the actual work:

* [strimpack](https://github.com/j4p3/strimpack) webserver producing main website, handling authentication, payments, and client application prerendering
*  [strimchat](https://github.com/j4p3/strimchat) chatserver for client application
*  [strimpack web client](https://github.com/j4p3/strimpack-web-client) react app for main site

The application also uses other open source projects:

*  [discourse](https://github.com/discourse/discourse) forum application
*  redis
*  postgresql


## usage

**Can I configure this to match the way I want it to be?**

Sure. So far you can adjust the following items to suit you:

* Stream title
* Primary theme color
* Stream logo
* Subscription levels
* Subscription prices
* Stream location

And Discourse, the software powering the forum, has a whole slew of configuration options, too.

**Who made this and why?**

[I made this for fun](https://bonner.jp/work), and because livestreaming seems to be getting popular but it's difficult to stand up a page for it on your own. And because the livestreaming platforms take an egregious chunk of the money people tip streamers, even after they've ground their way to "partnered" status. And to learn a bit about Docker Compose while I'm interviewing for jobs. Good grief, interviews are terrible.

**Given that this relies on Twitch's streaming engine, is there anything under the hood that's interesting from a technical perspective?**

There's a nice separation of server and client in that they share a volume created by docker-compose, rather than being in the same repo. (The server needs access to the client app so that it can render it before delivering the page.) I hate having a frontend single-page-app in the same repo as the server, and that was the solution I found.

It was also neat investigating and discarding all the options out there for chat servers - I ended up rolling my own because I preferred using websockets, not polling/BOSH.

I was very impressed with React's (finally official) Context API. If you want, you can do a lot of the same state management that you would otherwise require something like Redux, complete with predefined functions to mutate state based on user actions. But as the creators of Redux [have already pointed out](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367), many of the people using Redux don't actually need it - the indirection and the time-travel in particular solve a very broad scope of problems.

In general, though, the most interesting part of the concept is the idea of an open-source anti-platform as an alternative to big centralized marketplace-style platforms. With a bit of work on the Docker side and some opinionated hosting/DNS choices, this tool could be deployable with a credit card and a click. If you wanted to have the social/shared audience benefits of a platform, you could publish your instance and have a federated network of streamers running on the anti-platform.

**Can I use this if I'm not a programmer?**

Sure, but you'll need to be able to follow the steps below:

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

If you'd like to set up something like this, but don't think you'll be able to follow these instructions, feel free to reach out and I'll see if I can help.

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