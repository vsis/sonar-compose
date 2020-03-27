# Docker-compose project with sonarqube + postgresql + nginx + let's encrypt

## Step 1: Create SSL certificate and key

```
$ certbot certonly
```

## Step 2: Start project

```
$ docker-compose up -d
```

## Renew certificate

I'm a very lazy person. So, because I don't need the service being up while renewing certificate, I just shut down the service and then renew the certificate.

```
docker-compose down
certbot renew --dry-run
``` 
