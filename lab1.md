# App Dev: Setting up a Development Environment v1.1

## Overview
In this lab, you will provision a Google Compute Engine virtual machine and install software libraries for Node.js software development on Google Cloud Platform.

## Objectives
In this lab, you will learn how to perform the following tasks:

- Provision a Google Compute Engine instance.

- Connect to the instance using SSH.

- Install software on the instance.

- Verify the software installation.

## Setup
### Before you begin
use your Qwicklabs credentials to sign in to Google Cloud Platform Console.

### Activate Google Cloud Shell
Google Cloud Shell is a virtual machine that is loaded with development tools. It offers a persistent 5GB home directory and runs on the Google Cloud. Google Cloud Shell provides command-line access to your GCP resources.

1. In GCP console, on the top right toolbar, click the Open Cloud Shell button.

2. Click `Continue`.
> It takes a few moments to provision and connect to the environment. When you are connected, you are already authenticated, and the project is set to your PROJECT_ID.


### gcloud
gcloud is the command-line tool for Google Cloud Platform. It comes pre-installed on Cloud Shell and supports tab-completion.
> Full documentation of gcloud is available on [Google Cloud gcloud Overview](https://cloud.google.com/sdk/gcloud) .


## Task 1: Creating a Compute Engine Virtual Machine Instance

* create a vm instance
`gcloud beta compute --project=[PROJECT_ID] instances create dev-instance --zone=us-central1-a --machine-type=e2-medium --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --service-account=[SERVICE_ACCOUNT] --scopes=https://www.googleapis.com/auth/cloud-platform --tags=http-server --image=debian-10-buster-v20200902 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=dev-instance --no-shielded-secure-boot --no-shielded-vtpm --no-shielded-integrity-monitoring --reservation-affinity=any`

* set firewall rules
`gcloud compute --project=[PROJECT_ID] firewall-rules create default-allow-http --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http-server`

## Task 2: Install software on the VM instance
connect to the vm instance using `SSH`

2
1. In the SSH session, to update the Debian package list, execute the following command:
`sudo apt-get update`
2. To install Git, execute the following command:
`sudo apt-get install git`
3. To download the Node.js setup script, execute the following command:
`curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -`
4. To install npm and Node.js, execute the following command:
`sudo apt install nodejs`


## Task 3: Configure the VM to Run Application Software

1. Check the version of Node.js:
`node -v`
> You should see the Node.js version number for version 6.

2. Clone the class repository:
`git clone https://github.com/GoogleCloudPlatform/training-data-analyst`

3. Change the working directory:
`cd ~/training-data-analyst/courses/developingapps/nodejs/devenv/`

4. run a simple web server
`sudo node server/app.js`

5. Stop the application by pressing `Ctrl+C`.

6. Install the Node.js library for Compute Engine `npm install`

7. Run a simple Node.js application that lists Compute Engine instances
`node list-gce-instances.js`

## End your lab
When you have completed your lab, click End Lab. Qwiklabs removes the resources you’ve used and cleans the account for you.