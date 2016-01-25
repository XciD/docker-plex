# docker plex

This is a Dockerfile to set up (https://plex.tv/ "Plex Media Server") - (https://plex.tv/)

For the paid for plexpass version goto https://github.com/timhaak/docker-plexpass

Build from docker file

```
git clone git@github.com:timhaak/docker-plex.git
cd docker-plex
docker build -t timhaak/plex .
```

You can also obtain it via:

```
docker pull timhaak/plex
```

---
Instructions to run:

```
docker rm -f plex
docker run -d --name plex \ 
              --restart=always \ 
              -e PLEX_USERNAME=*YOURPLEXUSERNAME*  \
              -e PLEX_PASSWORD=*YOURPLEXPASSWORD*  \ 
              -h *your_host_name* \ 
              -v /*your_config_location*:/config \ 
              -v /*your_videos_location*:/data \ 
              -p 32400:32400  timhaak/plex 

```

If you change the standard port output, dont forget add ``PLEX_EXTERNALPORT`` as ENV Variable to setup the new port
```
docker run -d --name plex \ 
              --restart=always \ 
              -e PLEX_USERNAME=*YOURPLEXUSERNAME*  \
              -e PLEX_PASSWORD=*YOURPLEXPASSWORD*  \ 
              -e PLEX_EXTERNALPORT=33400  \
              -h *your_host_name* \ 
              -v /*your_config_location*:/config \ 
              -v /*your_videos_location*:/data \ 
              -p 33400:32400  timhaak/plex 
```

There is also an option of ```--env=SKIP_CHOWN_CONFIG=TRUE``` that will let the Plex server load faster by skipping the permissions check. You can insert this as such: ```docker run --env=SKIP_CHOWN_CONFIG=TRUE``` rest of command

Start the docker instance again and it will stay as a daemon and listen on port 32400.

Browse to: ```http://*ipaddress*:32400/web``` to run through the setup wizard.
