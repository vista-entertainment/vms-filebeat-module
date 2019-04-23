# Vista Software filebeat module

Contains the filebeat module that can be used with filebeat to forward logs to elasticsearch

## How to configure filebeat to forward logs

### Install with Chocolatey (Windows)

`choco install filebeat`

### Configure filebeats to use the module

Ensure the config points to **modules.d** directory 

    filebeat.config.modules:
      path: ${path.config}/modules.d/*.yml

Copy the vista module folder inside **modules** to make it available to in Filebeat.

Copy the module configuration metadata vista.yaml inside **module.d** folder

Enable the module:

`.\filebeat.exe modules enable vista`

ensure it is enabled with 

`.\filebeat.exe modules list`

### Setup the pipeline

`.\filebeat.exe setup --modules vista --pipelines`


### Optional: Set the paths variableedit
The examples here assume that the logs you’re harvesting are in the location expected for your OS and that the default behavior of Filebeat is appropriate for your environment.

Each module and fileset has variables that you can set to change the default behavior of the module, including the paths where the module looks for log files. You can set the path in configuration or from the command line. For example:

- module: vista
  log:
    var.paths: ["C:/ServiceFramework/*.log"] 

### Start filebeat 

via command line

`.\filebeat.exe --c .\filebeat.yml -e`

or as a service

Start-Service filebeat

## How to setup a (minimal) ELK stack to test pipelines

	version: '2.0'
	services:
	  elasticsearch:
	    image: docker.elastic.co/elasticsearch/elasticsearch:7.0.0
	    container_name: elasticsearch
	    environment:
	      - node.name=elasticsearch
	      - discovery.type=single-node
	    volumes:
	      - /usr/share/elasticsearch/data
	    ports:
	      - 9200:9200
	
	  kibana:
	    image: docker.elastic.co/kibana/kibana-oss:7.0.0
	    ports:
	      - "5601:5601"
	    depends_on:
	      - elasticsearch
	