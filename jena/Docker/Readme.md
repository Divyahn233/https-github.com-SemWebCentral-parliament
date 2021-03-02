# Parliament Docker

 
#### Building
##### Windows
If you have already built parliament in a Windows OS just call ant:

    ant
Otherwise specify the url to the Parliament RedHat build first in the variable "parl_url" (Note: for the above, make sure parl_url is not set!) and the version in the variable "parl_version":

    set parl_url=https://github.com/SemWebCentral/parliament/releases/download/release-2.7.13/Parliament-v2.7.13-msvc-64.zip
    set parl_version=2.7.13
    ant build-win

If "https_proxy" has been set as an environment variable, the ant script will use the proxy for building (only).

##### RHEL8
If you have already built parliament in a RedHat 8 OS just call ant:

    ant
Otherwise specify the url to the Parliament RedHat build first in the variable "parl_url" (Note: for the above, make sure parl_url is not set!) and the version in the variable "parl_version":

    export parl_url=https://github.com/SemWebCentral/parliament/releases/download/release-2.7.13/Parliament-v2.7.13-gcc-centos7-64.zip
    export parl_version=2.7.13
    ant build-rhel8

##### Ubuntu   
Specify the url to the Parliament RedHat build first in the variable "parl_url" and the version in the variable "parl_version":

    export parl_url=https://github.com/SemWebCentral/parliament/releases/download/release-2.7.13/Parliament-v2.7.13-gcc-ubuntu18-64.zip
    export parl_version=2.7.13
    ant build-ubuntu
   
## Load Parliament Image
You can load the factory built images by downloading one of the docker image *-docker.tar.gz files from github, or if you built a new container, it will be found in target/distro directory.  Load locally using:

    docker load -i parliament-rhel8-2.7.13.tar.gz

Verify it was loaded with:

    docker image ls

## Running Parliament

Parliament publishes to port 8089 in the container. You will need to map a local port you need to run it on using the run command.  E.g., to run it locally on port 80 you would use the following:

    docker run --name parliament -rm -dip 80:8089 parliament-rhel8-2.7.13

You can (should) also run it with a local directory used for persistent storage (this recommended, otherwise it will reset when the container shuts down). Create your directory and map it as follows:

    mkdir -p C:\data\kb-data
    docker run --name parliament --rm -dip 80:8089 -v C:\data\kb-data:/usr/local/Parliament/kb-data parliament-rhel8-2.7.13

or for a Windows container:

    docker run --name parliament --rm -dip 80:8089 -v C:\data\kb-data:c:\Parliament/kb-data parliament-win-2.7.13
     
If you need to connect to running parliament container:

    docker exec -it parliament cmd.exe

To stop the running container use:  

    docker stop parliament
Note: if you have not set up a volume for persistent storage (mapped to "Parliament/kb-data" as above), all data will be lost when it is stopped.
