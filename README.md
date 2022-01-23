# ultimatemediaserver
- This is a collection of docker containers that work in tandem to provide what I believe to be the ultimate home media server.
- You can follow along with the Videos in this playlist: https://www.youtube.com/playlist?list=PLuIcyDQjJwFoxputJfMey3EIkhMYl6fY0
- There are two Scripts in the Repo, if you already have a docker environment setup you can just use the docker-compose file that has all the paths and variables pre-mapped.
- This is an example of a service within a docker compose file:

 # docker-compose
 
    appname: // This is just a header for the docker environment to divide the containers
    image: imageurl // This is the image url that docker will pull to build the container
    container_name: appname // This will be the name seen in portainer and the docker cli
    environment: // these are env. variables that can change what the container does
      - PUID=0 // This is a user code giving the container the access of a root user, this DOES NOT mean the container can access the main machine just makes interlinking easier.
      - PGID=0 // Same as above but this is the group variable.
      - TZ=Europe/London // Time Zone, not all containers have this and in my experience its just about useless as this can be set within the container 9/10 times
    volumes: // Volumes are where the container will store data in relation to the HOST Machine. The format is /PathOnHost:/PathInContainer
      - /dockerconfig/appname/config:/config // For Ease of use, troubleshooting and possible cloning I store all the containers in a created folder so all files can easily be accessed on the host
    ports: // Ports that the container will use in the format of: - PortOnHOST:PortinContainer | This can be used to change the port on the host to avoid port conflicts but most 
    containers will just let you change the whole string ex. 1111 on the host could point to 1234 in that container. But most containers ive come across will just let you do 1111:1111
      - 1234:1234 
    restart: unless-stopped // This is the restart policy and can be changed later.

  # More Info 
    
- The second script is an .sh file and what it does is install docker and docker-compose as well as fetch the compose file from this repo and run it. This basically is a one command 
 way to build a full docker service. Great for noobs.
 
- The chosen management software for Docker is Portainer. It's simple to use and allows you to manage your containers easily. It also provides a great learning experience to learn docker.
 Alternatively you can change this or forgo it in favor of the CLI but the choice is yours.
- For Movies and TV Show Management I have opted for Radar and Sonar respectively.
- There are two download clients provided depending on your use. For torrents I opted for deluge and for NZB I opted for SABNZBd.
- NGINX Proxy Manager was added so that all containers can be accessed securely over the web without port forwarding. You will need a domain for this (but they are cheap and it
 makes it so much cooler)
- Ombi is an API connection that allows one user interface for adding movies and tv shows
- You will notice I did not include a media front end. Personally I like and use Plex but many prefer Emby and with both being very simple to install I opted to not include either in
 this script. 
  # Installing
 - INSTALL INSTRUCTIONS FROM THE SH SCRIPT
 you will need a linux machine with root access or the windows subsystem for linux installed to use the script (Sorry Mac Guys)
 simply run wget https://raw.githubusercontent.com/DylanManiatakes/ultimatemediaserver/main/dockermediaserver.sh
 This will download the script to the current directory you're in (Probably /home/user unless you changed your working dir.)
 After this run sudo chmod u+x dockermediaserver.sh, enter your password and once complete run sudo ./dockermediaserver.sh
 This will download and install docker and its dependencies as well as automatically wget the docker-compose file and run it.
 Log in to Portainer at HOSTIP:9000 and you can start the setup process and see all containers.
 
 
 - INSTALLING ON EXISTING DOCKER ENV.
 Simply download the docker-compose file from https://raw.githubusercontent.com/DylanManiatakes/ultimatemediaserver/main/docker-compose.yml and run it
 -In linux this will be done by running wget https://raw.githubusercontent.com/DylanManiatakes/ultimatemediaserver/main/docker-compose.yml and then sudo docker-compose up
 -In Windows this can be done using the docker UI or command prompt in CMD type "bash" and it will open up a linux shell in windows. run the same command as above and it should 
 work its magic.
 NOTE if you already have any of the containers in the compose file it will error out due to conflicts.
 
 - Updating
 I have had problems with watchtower, docker container that can auto update however if you ever want to check for updates or just force an update you can run 
 sudo docker-compose up again. This will not overwrite your existing configs but it will check for new images and pull them if there are new versions. 
 This can also be done within portainer under the stacks tab. "stacks" in portainer is basically docker-compose with a gui. 
 
 - ADDING MORE CONTAINERS
 You can add more containers as you see fit in portainer but I would recommend adding them using the docker-compose file only because it will teach you more of the workings of
 docker but also keep those containers updated with the rest. 




