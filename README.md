# Portainer

Portainer is a tool with a GUI and accessed via browser. It's used to manage images, containers, volumes, networks and other Docker funcionalities. It has two versions: Business Edition (BE) and Community Edition (CE).

In this documentation, it will be explained how to install the Community Edition and yours configuration.

## Step 1 - installation

We will use Docker to run Portainer, simple and pratical. Generally, your installation is very simple, requiring only some steps.

The first step is to rename the **nginx/conf.d/portainer.conf_example** file to **nginx/conf.d/portainer.conf** and change the parameters correctly.

Then, deploy Portainer:

```shell
docker-compose up -d
```

## Step 2 - upgrade

To upgrade Portainer, just change the version of it in docker-compóse.yml file

```yml
...
...
  portainer:
    image: portainer/portainer-ce:2.16.1 #change version here
    command: -H unix:///var/run/docker.sock
...
...
```

Then, execute the following command;

```shell
docker-compose up -d
```

## Step 3 - reset admin password

If you want to reset the admin password of Portainer, just follow the tutorial:

First stop the Portainer container:

```shell
docker stop portainer
```

Then, give 777 permission to the following file:

```shell
chmod 777 /var/lib/docker/500000.500000/volumes/portainer_data/_data/portainer.db
```

Use the Portainer Tool for reset the admin password:

```shell
docker run --rm -v portainer_data:/data portainer/helper-reset-password
```

The output must be something like this:

```
2022/11/19 12:13:58 Password successfully updated for user: admin
2021/11/19 12:13:58 Use the following password to login: &_4\3^5V8vLTd)EdloSjts26Gb9HPl1
```

Finally, change again the portainer.db permission and start Portainer:

```shell
chmod 600 /var/lib/docker/500000.500000/volumes/portainer_data/_data/portainer.db

#Start container container:
docker start portainer
```

Step 4 - accessing

After install, access Portainer via browser


For http: http://ip_potainer:9000/

For https: https://hostname_portainer:9000/

**PS:** if this is your first access, just create a strong pasword for the admin user. If you already have a user registered (in case of upgrade, for example), just access it using your existing credentials