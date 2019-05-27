# Getting started with MOSIP Pre-Registration User Interface

Eager to try out the mosip pre-registration module? Here are the instructions for setting it up and giving it a spin. Deploying mosip involves building and creating deployable images of the software, setting up dependencies, updating the configuration and creating a kubernetes cluster and running the mosip micro services on it. The following sections will address these in steps.

/mosip-infra/scripts/build-deploy has scripts for setting up the environment, the build box and the actual build scripts. The environment folder has scripts that can be run to setup the dependencies for mosip such as antivirus, ldap, postgres, nginx proxy, hdfs and ssl certificate. The dependencies required can be setup in either a single VM or multiple Virtual Machines. Each of the services described can be hosted separately.


## Setup Dependency Environment

mosip uses postgres to store data, hdfs to store files, and ldap for authorization information. In addition to these the file service requires an external virus scanning service. Since the microservices are deployed on a kubernetes cluster, a proxy service is also needed to forward requests as well as handle https. Let us setup each of these one by one.

The scripts referred to in the sections below are for a RHEL/CentOS 7.6 environment. If you choose alternate environments your setup process might vary. Also the scripts prompt the running of manual commands in places. These instructions are to be followed to complete the setup as intended.


### Setting up postgres database

Refer to the steps in the script psql-setup.sh for setting up your postgres server. It is recommended that you follow the script as closely as possible to keep configuration changes to a minimum.

### Setting up hdfs

Refer to the steps in the script hdfs-setup.sh for getting your hdfs environment up and running.

### Setting up antivirus

Refer to the steps in the script clam-setup.sh to setup clam antivirus on a virtual machine.

### Setting up ldap

Refer to the steps in the script ldap-setup.sh to setup Apache Directory Services as your ldap provider.

### Proxy setup

NGINX is used as the proxy. It has to be setup with SSL support. Use the following scripts to set these up. Follow the steps in proxy-setup.sh and then ssl-setup.sh to get your proxy running.

### Kubernetes setup

We used the Azure kubernetes service and setup a cluster with 5 nodes. The nodes had 4 vcpus and 8 GB RAM each. We recommend that you try the same. You are however free to use any kubernetes environment with your own node configurations.

### Setting up the Key Manager

The Key Manager is used to save Private and Public Keys used for encryption in mosip. This uses SoftHSM and can be setup in a separate VM. Follow the instructions in the keymanager-setup.sh script.


## Building mosip

Refer to the readme section in the root forlder of the repo for instructions in building the mosip code. The output of the build process will be docker images that can be deployed along with configuration.


## Configuration the system before running

In order to deploy mosip the configuration has to be first updated to point to the mosip environment. Additionally the docker deployment instructions for the kubernetes setup have to point to the correct cluster and the corresponding docker images.

### Database setup

The postgres database created earlier needs to be configured as follows:

* Creation of Roles

Create the users/roles specified here in the postgres database

#ToDo fill user creation information

* Creation of Schemas

Create the schema by running the following scripts in the order specified.

#ToDo specify list of sqls to be run

Please note that the order of execution of these scripts is important. The command to run these scripts is as follows.

#ToDo specify example of the command


* Creation of Seed Master Data

Import seed data into the system by running the following set of commands.

#ToDo specify the list of import commands to be run.


### Application configuration setup

mosip has a configuration server which holds the property files for the micro-services. These files contain information relating to access of dependency services and the deployment environment. These configuration entries have to be suitably modified to reflect your environment for the software to work. Given below is a list of configuration changes that need to be done.

#ToDo Add configuration update details here


### Kubernetes configuration

The following configuration updates have to be made in the yaml files in the kubernetes folder.

#ToDo Add the configuration steps to this section.



