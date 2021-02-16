---
layout: post
title:  "Docker, Run it all in a container"
categories: ['Docker']
---

Making a script that fires up everything a application needs, on your  machine for development and production!

https://mariadb.com/kb/en/installing-and-using-mariadb-via-docker/

Create a docker-compose.yml and describe every bit of your applications dependencies to make it run and then fire it up with the following command:

```
sudo docker-compose up -d
```

We need to know what IP Address docker assigned our container. Here is how I discovered it for my mariadb container:
```
{% raw %}
sudo docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ci_db_1
{% endraw %}
```