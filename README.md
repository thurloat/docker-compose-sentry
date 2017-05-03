# docker-compose-sentry

Creates a secure sentry deployment using docker compose that uses letsencrypt
to generate some certs for you automatically.

## setup

replace all your example.coms with your actual domain / subdomain of your
sentry server.

disable the https portion of the nginx config until the certs are generated
with letsencrypt

copy `env.*.sample` to `env.*`, and fill in your variables

`docker-compose up -d`
