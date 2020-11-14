Installing And Setup Streamsets Using Podman For Centos 8

Installing_And_Setup_Streamsets_Using_Podman_For_Centos_8.MD

https://github.com/streamsets/datacollector

StreamSets Data Collector is open source software for building dataflows quickly and easily, spanning on-premises, multi-cloud and edge infrastructure.

It has an advanced and easy to use User Interface that allows data scientists, developers and data infrastructure teams easily create data pipelines in a fraction of the time typically required to create complex ingest scenarios.

To learn more, check out http://streamsets.com

#***#

Step 0:

Add in /etc/hosts of the server ip address for datacollector, example ip - Change yours

192.168.0.10 datacollector 

Step 1 : Install Podman 
 
dnf install podman-docker

#***#

Step 2 : Create the needed volume.

podman create -v /logs --name sdc-logs_container streamsets/datacollector:latest
podman create -v /etc/sdc --name sdc-conf_container streamsets/datacollector:latest
podman create -v /opt/streamsets-datacollector/streamsets-libs --name sdc-libs_container streamsets/datacollector:latest
podman create -v /data --name sdc-data_container streamsets/datacollector:latest

#***#

Step 3 : Run this if you need to edit config file (you may skip this step)

podman run --rm -it --volumes-from sdc-conf_container ubuntu bash

#***#

Step 4 : Run the command in one continues line

podman run --name sdc -d --privileged --restart on-failure --name datacollector -h datacollector -p 18630:18630 --env SDC_CONF_http_authentication=form -v sdc-libs_container:/opt/streamsets-datacollector/streamsets-libs -v sdc-data_container:/data -v sdc-logs_container:/logs -v sdc-conf_container:/etc/sdc -P streamsets/datacollector:latest dc -verbose

#***#

Step 5

To check the podman container

podman ps -a

Wait for 60 seconds for the container to prepare.

Step 6 : Edit hosts file for your OS of your browser. (Windows or Linux)

Add in hosts file of the server ip address for datacollector, example ip - Change yours

192.168.0.10 datacollector 

#***#

Step 6 : Using Firefox browser visit https://accounts.streamsets.com

Register your self

#***#

Step 7: From the same browser, open a new tab and visit

http://datacollector:18630

Login with Streamsets default user admin and password admin. You must change your password. 


Optional:-

Use the command to check /etc/hosts and other settings.

podman exec -it datacollector /bin/bash

#***#

Link for references

https://hub.docker.com/r/streamsets/datacollector
 
https://streamsets.com/blog/getting-started-streamsets-data-collector-docker/

http://thecloudnative.com/Streamsets-Development-Setup/


Harisfazillah Jamel

https://www.facebook.com/isdomy

ICT Service Delivery And Operation - ISDO

==========
