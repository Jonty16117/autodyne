[![Docker Image CI](https://github.com/compsecdirect/autodyne/actions/workflows/docker-image.yml/badge.svg?branch=main)](https://github.com/compsecdirect/autodyne/actions/workflows/docker-image.yml)
[![Docker Image CI Develop](https://github.com/compsecdirect/autodyne/actions/workflows/docker-image-develop.yml/badge.svg?branch=develop)](https://github.com/compsecdirect/autodyne/actions/workflows/docker-image-develop.yml)
![alt text](https://github.com/compsecdirect/autodyne/blob/main/Autodyne-CompSecDirect.png "Autodyne logo")  

# Autodyne: Automated firmadyne by CompSec Direct

## Purpose

Improve Firmadyne (https://github.com/firmadyne/firmadyne) and make it simpler to extract, emulate firmware for analysis.  

## Usage

1. Get firmware samples to analyze. Add firmware to ```samples``` folder
2. Edit the ```docker-compose.yml``` to include the desired "Manufacturer name" (can be anything) and path to samples.  
a. ```command``` section has  "foo", "1.bin" ; this is the "Manufacturers Name" and file name.  
b. ```volumes``` section has path to firmware samples and mapping to local images.  
3. Copy the relevant sections multiple times (given x samples).  
a. copy section from ```emulator-1``` until next entry.   
b. manually increment the desired ip address.  
4. ```make build and make start```  
5. ```docker exec CONTAINERID bash```  
6. ```tmux ls```  
7. ```tmux a -t "ImageID X"```  Where X is the database id generated by firmadyne.  
a. This tmux session is the console session to the firmware sample.
8. To view the web interface on your host machine, follow these steps. Check the URL in the container logs. Look at line 6 in the file ```./nginx-config/{EMULATED_CONTAINER_NAME}/default```. If the URLs are different:  
a. Update the IP address at line 6 in ```./nginx-config/{EMULATED_CONTAINER_NAME}/default``` with the IP address from the container logs.  
b. Restart Nginx by running the command ```service nginx restart``` from inside the container.  
If the URLs are the same:  
c. Go to ```http://localhost:<PORT>``` to see the web page of the firmware.  
*(Note: Replace ```<PORT>``` with the specific port number from the respective container's Docker Compose configuration.)*  

## Notes

0. main branch is ubuntu 18.04 / dev branch is ubuntu 20.04 base images.  

1. If you did not get a tmux session; a failure occurred during the seven firmadyne steps. We keep a ```samples-out``` folder to collect and debug emulation efforts.  
bin-extractor-output  
bin-getArch-output  
bin-inferNetwork-output  
bin-makeImage-output

## Authors
o Charles Boyd  
o DJ Forbes
