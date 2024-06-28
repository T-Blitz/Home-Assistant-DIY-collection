### Info for This folder


Currently this repo assume that you have basic Docker and linux understanding, in the future this repo shall be updated to include a full walk-through.
This is a simple Docker set up to use a light weight and easy to replicate and bakup Hass setup.
Just copy the HassServer folder asa bakup and use the DockerCompose file to set everything up again.

This setup assume you are using a Debian / Ubuntu / RassberryOS with [CasaOS](https://casaos.io) installed. I higly recommend doing so, since the CasaOS web UI makes file transfair way easier.
Also there is no need to install docker manulally, since it comes with CasaOS. Portainer can be istalled through the WebUI (recommended). How ever i do not recommend installing Home Assistant through said UI APP Store
but with my Docker Compose.

If you are having trouble with connecting your MQTT to the sh shell, then please try to downgrade docker engine. As it seems to be currently bugged (stand 28.Jun 2024)
