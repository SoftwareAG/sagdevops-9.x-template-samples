# Integration Server default provisioning template

## Capabilities

You can use this template to provision variety of environments with core Integration Server instance.
Such environments can be used as a foundation for layered products and more complex environments that
require Integration Server layer.

The template can be used as is, or cloned and customized to your needs.

DO NOT MODIFY this template! Your changes WILL BE LOST.

## Requirements and Compatibilities

* Command Central version 9.10+
* Integration Server version 9.8+
* Supported Database Server (Oracle, SQLServer, DB2)
* Target host on supported Windows or UNIX system with SSH access
* Valid Integration Server 9.x license key for your target platform

## Limitations



# Use Cases

The template can be applied using a single command that takes input parameters from a .properties file

    cc exec templates composite apply is-layer -i sample_is_oracle.properties

The set of properties in the properties file depends on the specific provisioning use case.
Below are some typical examples.


## Provision latest dev Integration Server from Empower/SDC without a database

This is the easiest environment type to get started with if you want to install locally on 
a machine that has Internet access and you have Empower/SDC credentials.

You will need:

* webMethods-${version} and Empower master repositories. Alternatively you can setup image/mirror repos.
* Valid Integration Server license key alias uploaded to Command Central 
* Free disk space for new installation folder

    cc exec templates composite apply is-layer \
       environment.type=dev \
       repo.product=webMethods-9.10 \
       repo.fix=Empower \
       is.license.key.alias=Integration_Server910 \
       install.dir=C:/new/install/dir
       
 
## Provision single Integration Server with Oracle database

Make a copy of sample.properties file and customize it to your needs.

Execute with 'server' environment.type and is.host parameter:

    cc exec templates composite apply is-layer -i sample.properties \
       environment.type=server \
       is.host=ccdemowin2012 \

    
## Provision layer of unclustered of Integration Servers

Execute with 'layer' environment.type and a list of is.hosts:

    cc exec templates composite apply is-layer -i sample.properties \
       environment.type=layer \
       is.hosts=[bgcctbp12,bgcctbp13] \
       os.platform=lnxamd64       

    
## Provision Integration Server cluster with Terracotta Server

You MUST have Terracotta Server or Array ready and accessible. See tc-layer template on how to setup one.

Execute with 'cluster' environment.type and a list of is.hosts, and point to the TSA:

    cc exec templates composite apply is-layer -i sample.properties \
       environment.type=cluster \
       is.hosts=[bgcctbp12,bgcctbp13] \
       os.platform=lnxamd64 \
       is.tsa.url=bgcctbp12:9910 \
       tc.license.key.alias=Terracotta \
