**Installing And Setup Streamsets Using Podman For Centos 8**


StreamSets Data Collector is open source software for building dataflows quickly and easily, spanning on-premises, multi-cloud and edge infrastructure.

 
It has an advanced and easy to use User Interface that allows data scientists, developers and data infrastructure teams easily create data pipelines in a fraction of the time typically required to create complex ingest scenarios.

 
To learn more, check out [https://github.com/streamsets/datacollector](https://github.com/streamsets/datacollector)

**Step 0:**


Add in /etc/hosts of the server ip address for datacollector, example ip - Change yours


192.168.0.10 datacollector


**Step 1 : Install Podman**

`dnf install podman-docker`


**Step 2 : Create the needed volume**.

  

`podman create -v /logs --name sdc-logs\_container streamsets/datacollector:latest`

  
`podman create -v /etc/sdc --name sdc-conf\_container streamsets/datacollector:latest`

  
`podman create -v /opt/streamsets-datacollector/streamsets-libs --name sdc-libs\_container streamsets/datacollector:latest`

  
`podman create -v /data --name sdc-data\_container streamsets/datacollector:latest`

  
**Step 3 : Run this if you need to edit config file (you may skip this step)**

`podman run --rm -it --volumes-from sdc-conf\_container ubuntu bash`


**Step 4 : Run the command in one continues line**


`podman run --name sdc -d --privileged --restart on-failure --name datacollector -h datacollector -p 18630:18630 --env SDC\_CONF\_http\_authentication=form -v sdc-libs\_container:/opt/streamsets-datacollector/streamsets-libs -v sdc-data\_container:/data -v sdc-logs\_container:/logs -v sdc-conf\_container:/etc/sdc -P streamsets/datacollector:latest dc -verbose`


**Step 5**


To check the podman container


`podman ps -a`


Wait for 60 seconds for the container to prepare.


**Step 6 : Edit hosts file for your OS of your browser. (Windows or Linux)**


Add in hosts file of the server ip address for datacollector, example ip - Change yours

192.168.0.10 datacollector


**Step 7 : Using Firefox browser visit https://accounts.streamsets.com **

Register your self

  

**Step 7: From the same browser, open a new tab and visit**


http://datacollector:18630


Login with Streamsets default user admin and password admin. You must change your password.

  

**Optional:-**

Use the command to check /etc/hosts and other settings.


`podman exec -it datacollector /bin/bash`

  

Link for references

[https://hub.docker.com/r/streamsets/datacollector https://streamsets.com/blog/getting-started-streamsets-data-collector-docker/](https://hub.docker.com/r/streamsets/datacollector https://streamsets.com/blog/getting-started-streamsets-data-collector-docker/)

[http://thecloudnative.com/Streamsets-Development-Setup/](http://thecloudnative.com/Streamsets-Development-Setup/)


Harisfazillah Jamel

[https://www.facebook.com/isdomy](https://www.facebook.com/isdomy)


ICT Service Delivery And Operation - ISDO
