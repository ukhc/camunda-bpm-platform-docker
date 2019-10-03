# Camunda BPM Platform for Docker and Kubernetes

## Reference
- https://hub.docker.com/r/camunda/camunda-bpm-platform
- https://github.com/camunda/docker-camunda-bpm-platform/blob/master/README.md

## Docker deployment to the local workstation

~~~
# start the container
docker run -d --name camunda -p 8080:8080 camunda/camunda-bpm-platform:latest

# see the status
docker container ls

# open the url
open http://127.0.0.1:8080/camunda-welcome/index.html

# destroy the container
docker container stop camunda
docker container rm camunda
~~~


## Kubernetes deployment to the local workstation (macOS only)

## Prep your local workstation (macOS only)
1. Clone this repo and work in it's root directory
1. Install Docker Desktop for Mac (https://www.docker.com/products/docker-desktop)
1. In Docker Desktop > Preferences > Kubernetes, check 'Enable Kubernetes'
1. Click on the Docker item in the Menu Bar. Mouse to the 'Kubernetes' menu item and ensure that 'docker-for-desktop' is selected.

NOTE: Run the following commands from the root folder of this repo.

### Deploy Camunda BPM Platform
~~~
./local-apply.sh
~~~


### Create a backup of the database
~~~
./local-backup.sh
~~~

This backs up the database. The backup will be created in the 'backup' folder in this repo. You can take multiple backups.


### Delete the deployment
~~~
./local-delete.sh
~~~


### Restore from backup (pass it the backup folder name)
~~~
./local-restore.sh 2019-10-31_20-05-55
~~~

Restore from one of your backup folders to populate the database.  The backups are stored in the 'backup' folder in this repo.


### Restart the deployment
~~~
./local-restart.sh
~~~

Some changes may require a restart of the containers.  This script will do that for you.


### Scale the deployment
~~~
kubectl scale --replicas=4 deployment/camunda-bpm-platform
~~~


### Shell into the container
~~~
./local-shell-camunda-bpm-platform.sh
~~~


### Get the logs from the container
~~~
./local-logs-camunda-bpm-platform.sh
~~~