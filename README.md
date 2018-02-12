# Pocketmine for Docker
An updated fork of [nmarus/docker-pocketmine](https://github.com/nmarus/docker-pocketmine), a Docker wrapper of the Pocketmine-MP Minecraft server for Minecraft PE and Bedrock (better together editions) clients. 
This fork adds a simple build script, updated base image (CentOS 7), and pulls the updated [installation script](https://get.pmmp.io).

## Requirements
* Download and install the appropriate [Docker installation](https://www.docker.com/) for your system (the host)
* Open server port in host firewall (default 19132) ([Windows](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access),[Linux](https://help.ubuntu.com/lts/serverguide/firewall.html))
* Enable C drive sharing in [Docker Settings](https://beta.docker.com/docs/windows/getting-started/#docker-settings)  
* (Optional) a [git client](https://git-scm.com/downloads) if cloning the repo

## Getting Started
One time setup:
* Clone this repository or download it
* In the repo folder, run  
        <pre>build</pre>
* The rebuild script will:
	* Delete old pocketmine images and containers on the host
	* Build the docker image with the latest Pocketmine (not published to dockerhub)
	* Create **pocketmine** the container
    
## Usage
### Configuration
By default, the **build** script will create a folder **USER_HOME/.pocketmine/data** where the server data will reside. This allows configuration and worlds to persist even if the docker container is erased.

The **server.properties** file under the **data** folder in the repo folder can be updated to configure the server prior to starting
Upon the first run, the server will populate the data directory

### Custom maps
To add maps, stop the server, rename the custom map directory to *world* (THIS IS IMPORTANT), then place it under:

    c:\users\myuser\.pocketmine\data\worlds\ 

For linux, use:

    /home/myid/.pocketmine/data/worlds

### Starting Pocketmine container:
If the container is stopped (run "docker ps -a" to verify), and you wish to start it, run: 

    docker start pocketmine

### Stopping Pocketmine container:
If you wish to stop the container in order to reboot the host os or update configuration files, run:

    docker stop pocketmine

### To interact with pocketmine administration:

    docker attach pocketmine
    
This allows you to jump into the pocketmine administration session. Type "help" for options. If you enter the command "stop", this will end pocket mine and stop the container. To restart pocketmine with our stopping the container, enter "restart" in the pocket mine admin session.
    
*To exit the admistration interface, press control-p, control-q. This is in order to maintain the container in service.*

### To view the logs in realtime run:

    docker logs -l pocketmine
    
This allows you to view the logs generated from the pocketmine server in a "tail -f" type format. 
    
*Press control-c to exit*

###To update minecraft pe to latest version:
Simply stop the pocketmine container and then start it. the latest version of pocketmine will be downloaded. 

*This assumes you are mapping your configuration to a directory external to the container. If not, you will lose your world...*

    docker stop pocketmine
    docker start pocketmine