# docker-compose-sentry

Creates a slim and secure sentry deployment using docker compose that leverages letsencrypt to generate SSL certs for you automatically.

All persistent data is stored in the ./data subdirectory for Letsencrypt, Postgresql, and Redis.

Adds the `SENTRY_DISABLE_REGISTRATION` to `sentry.conf.py` that can be configured via environment variables to more easily lock down registration on private servers.


## Dependencies

To prep an Ubuntu 16.04 server, instructions valid as of May 3, 2017.

```shell
sudo apt-get update && sudo apt-get dist-upgrade -y
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install docker-ce
wget https://bootstrap.pypa.io/get-pip.py
sudo python3 get-pip.py
sudo pip install docker-compose
git clone <this repo>
```

## Setup

Have a domain name ready, with DNS already configured to point to this server.

Copy `env.*.sample` to `env.*`, and fill in your variables, replacing references to `example.com`.

```shell
cp env/letsencrypt.sample env/letsencrypt
cp env/sentry.sample env/sentry
```

Copy `env.*.sample` to `env.*`, and fill in your variables, replacing references to `example.com`.

Replace references to `example.com` in your nginx.conf as well.

The default mail configuration points to `smtp.sparkpostmail.com`, feel free to use whatever else. Choose something where you have DKIM and SPF configured, so your alert emails are most likely to be delivered.


```shell
docker-compose up -d
docker-compose run --rm sentry-web sentry upgrade
# follow prompts to configure superuser, etc.
```

Log in to your new sentry server at https://sentry.example.com

## Notes

Please back up your data in the ./data directory, and your secret key off-site.
You don't want to lose those :grin:
