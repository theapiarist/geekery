---
title:
created:
updated:
draft: "false"
tags:
  - docker
  - raspberrypi
  - linux
  - software
---
Most instructions for running Pihole using Docker set the password as an environment variable in `compose.yml`. It's in this section:

```
    environment:
      TZ: 'Europe/London'
      FTLCONF_webserver_api_password: ''
      FTLCONF_dns_listeningMode: all
```

You can set the password as a blank (as above) from the outset, then run 

```
$ docker compose up -d
``` 

which will start the pihole container with no password set.

If you have one set already, you can change the password on a running container by determining the `docker container id` for Pihole (it's the first field generated from `docker ps -a`, and then use the following command to set the new password (or delete the password altogether):

```
$ sudo docker exec -it "ContainerID" pihole setpassword
Enter New Password (Blank for no password): 
  [✓] Password Removed
$
```

If you delete the password altogether it will be reset to whatever is in the environment variable when the container is restarted, unless you also edit the `compose.yml` file.