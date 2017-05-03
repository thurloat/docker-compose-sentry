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


## dependencies

To prep an Ubuntu 16.04 server, instructions valid as of May 3, 2017.

```
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
mkdir sentry
git clone <this repo>
```

