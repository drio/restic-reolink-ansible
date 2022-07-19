## Ansible playbook to boostrap mosquitto and home assistant

This is an ansible playbook that installs mosquitto (MQTT broker) and
hass.

I created this repo to make sure I can restore my home hass/mqtt setup
quickly. All my IOT devices use MQTT and I control them via HASS. Those
to services are crucial to my home network.

I started using those services and configuring them manually in a server. The
system was too fragile. I thought it'd be painful to rebuild the stack if
something happened to my server.

The harddrive on my server started to fail. So I decide to build this playbook.

## How to use it

We have to docker-compose services: hass and mosquitto. 

1. Drop your configs in the `dc/{mosquitto,hass-config}` directories. 
The hass-config is the set of files you get when you run a backup in hass. Or
when you copy the config dir in a hass instance.

Feel free to use the `./scripts/restore-hass.sh` script to extract a hass 
backup file into `./dc/hass-config`.

2. Run the boostrap.yml playbook:

`$ make boostrap`

This will install docker and docker-compose, sync up the local docker-compose
directory and start the services.

At this point mosquitto and hass should be running with your configs.

## Notes

As you can see from the docker-compose file, we are mounting a few
volumes for each of the services. The purpose of that is to be able
to control the service configuration from outside the containers.

In my mosquitto config, I also setup a couple of login/passwd for
authentication.

For hass, I already had a working instance so I created a backup (you can do so
via the hass UI) and restore it in the docker-compose service directory. Then
when the hass container starts, it will use that config. If you start fresh,
leave it empty. But remember to backup your config regularly.

### References

  1. https://github.com/josefmtd/mosquitto-docker
  2. https://blog.feabhas.com/2020/02/running-the-eclipse-mosquitto-mqtt-broker-in-a-docker-container/#Run_the_docker_image
