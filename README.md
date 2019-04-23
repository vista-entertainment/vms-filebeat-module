# Vista Software filebeat module

Contains the filebeat module that can be used with filebeat to forward logs to elasticsearch

## How to configure filebeat to forward logs

### Install with Chocolatey (Windows)

`choco install filebeat`

### Configure filebeats to use the module

Ensure the config points to **modules.d** directory 

    filebeat.config.modules:
      path: ${path.config}/modules.d/*.yml

Copy the vista module folder inside **modules.d** to make it available to in Filebeat.

Copy the module configuration metadata vista.yaml inside **module** folder

Enable the module:

`.\filebeat.exe module enable vista`

ensure it is enabled with 

`.\filebeat.exe module list`

### Setup the pipeline

`.\filebeat.exe setup --modules vista --pipelines`



### Start filebeat 

via command line

`.\filebeat.exe --c .\filebeat.yml -e`

or as a service

## How to setup a (minimal) ELK stack to test pipelines

