# Docker-compose project with sonarqube + postgresql + nginx + let's encrypt

This is a docker-compose project to make a sonarqube instance.

It uses postgresql, and nginx with a TLS certificate provided by [Let's Encrypt](https://letsencrypt.org)

## Requirements

You'll need

  - certbot
  - docker
  - docker-compose

## Step 1: Create SSL certificate and key

Make sure there's no process using port 80 in your host. Then use [certbot](https://certbot.eff.org/) to make a TLS certificate.

```
$ certbot certonly
```

## Step 2: Update certificate path

Open `nginx.conf`, then replace these lines:

```
    ssl_certificate /etc/letsencrypt/live/sonarjessy.ddns.net/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/sonarjessy.ddns.net/privkey.pem;
```

With:

```
    ssl_certificate /etc/letsencrypt/live/YOURHOST/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/YOURHOST/privkey.pem;
```

Where `YOURHOST` is the domain name of your certificate.

## Step 3: Start services

```
$ docker-compose up -d
```

## Renew certificate

I'm a very lazy person. So, because I don't need the service being up while renewing certificate, I just shut down the service and then renew the certificate.

```
docker-compose down
certbot renew
docker-compose up -d
``` 
