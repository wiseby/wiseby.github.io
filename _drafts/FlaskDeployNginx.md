---
title: Deploy on Rasbian
categories: [Linux, ServerSide]
---

update server system and install dependencies:

```
sudo apt update
sudo apt install python3-pip python3-dev build-essential libssl-dev libffi-dev python3-setuptools
```

Create the application and all nessecary conf files for uWSGI. Also supporting virtual envs using python3-env.

In your newly created environment install packages:

```
pip install uwsgi flask
```

Test the application using following command:

```
uwsgi --socket 0.0.0.0:5000 --protocol=http -w wsgi:app
```

We also need a .ini file to configure application for systemd:

```
nano path/to/project/project.ini
```

Enter the following save and quit:

```
[uwsgi]
module = wsgi:app

master = true
processes = 5

socket = myproject.sock
chmod-socket = 660
vacuum = true

die-on-term = true
```

now create a systemd file for the application:

```
sudo nano /etc/systemd/system/myproject.service
```

Enter the following replacing placeholders <> with your given filepaths and names:

```
[Unit]
Description=uWSGI instance to serve myproject
After=network.target

[Service]
User=<sammy>
Group=www-data
WorkingDirectory=</home/sammy/myproject>
Environment="PATH=</home/sammy/myproject/myprojectenv/bin>"
ExecStart=</home/sammy/myproject/myprojectenv>/bin/uwsgi --ini <myproject>.ini

[Install]
WantedBy=multi-user.target
```
