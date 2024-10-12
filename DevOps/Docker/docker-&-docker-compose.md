## Introduction
# The Docker Engine can run native Docker-style container workloads on Rocky Linux servers. This is sometimes preferred when running the full Docker Desktop environment.

## Add the Docker repository
# Use the dnf utility to add the Docker repository to your Rocky Linux server. Type:

```sudo dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo```

##  Install the needed packages¶
# Install the latest version of Docker Engine, containerd, and Docker Compose, by running:

``` sudo dnf -y install docker-ce docker-ce-cli containerd.io docker-compose-plugin```

## Start and enable Docker (dockerd)
# Use systemctl to configure Docker to automatically startup upon reboot and simultaneously start it now. Type:

``` sudo systemctl start docker ```
``` sudo systemctl --now enable docker ```

##  Optionally allow a non-root user to manage docker¶
# Add a non-root user to the docker group to allow the user to manage docker without sudo.

# This is an optional step, but it can be convenient if you are the system's main user or if you want to allow multiple users to manage docker but do not want to grant them sudo permissions.
# Type:

# Add the current user
```sudo usermod -a -G docker $(whoami) ```

# Add a specific user
``` sudo usermod -a -G docker custom-user ```
#  To be assigned the new group, you must log out and in again. Check with the id command to verify that the group has been added.

## Notes

# docker-ce               : This package provides the underlying technology for building and running docker containers (dockerd) 
# docker-ce-cli           : Provides the command line interface (CLI) client docker tool (docker)
# containerd.io           : Provides the container runtime (runc)
# docker-compose-plugin   : A plugin that provides the 'docker compose' subcommand ```


## Install git
``` sudo dnf install git ```
``` git --version ```


## Git colone
```git clone https://github.com/deviantony/docker-elk.git ```


## Bringing up the stack
# Clone this repository onto the Docker host that will run the stack with the command below:
``` git clone https://github.com/deviantony/docker-elk.git```

Then, initialize the Elasticsearch users and groups required by docker-elk by executing the command:
``` docker compose up setup ```

If everything went well and the setup completed without error, start the other stack components:
```docker compose up ```



The "changeme" password set by default for all aforementioned users is unsecure. For increased security, we will reset the passwords of all aforementioned Elasticsearch users to random secrets.
Reset passwords for default users
The commands below reset the passwords of the elastic, logstash_internal and kibana_system users. Take note of them.

```
docker compose exec elasticsearch bin/elasticsearch-reset-password --batch --user elastic
docker compose exec elasticsearch bin/elasticsearch-reset-password --batch --user logstash_internal
docker compose exec elasticsearch bin/elasticsearch-reset-password --batch --user kibana_system
```


Password for the [elastic] user successfully reset.
New value: ESugRsau=S09MxKUyIKE


Password for the [logstash_internal] user successfully reset.
New value: imvh4PVhOiiZOrYae2D-


Password for the [kibana_system] user successfully reset.
New value: mI-ivx=zLmDz_zZKtTP-



## Replace usernames and passwords in configuration files
```/opt/docker-elk
vim .env
```

## Restart Logstash and Kibana to re-connect to Elasticsearch using the new passwords
```
docker compose up -d logstash kibana
```

# Reference
``` https://github.com/deviantony/docker-elk ```


