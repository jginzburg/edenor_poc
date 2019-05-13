# Spring-Boot Camel QuickStart

This example demonstrates how you can use Apache Camel with Spring Boot.

The quickstart uses Spring Boot to configure a little application that includes a Camel route that triggers a message every 5th second, and routes the message to a log.

### Building

The example can be built with

    mvn clean install

### Running the example in OpenShift

It is assumed that:
- OpenShift platform is already running, if not you can find details how to [Install OpenShift at your site](https://docs.openshift.com/container-platform/3.3/install_config/index.html).
- Your system is configured for Fabric8 Maven Workflow, if not you can find a [Get Started Guide](https://access.redhat.com/documentation/en/red-hat-jboss-middleware-for-openshift/3/single/red-hat-jboss-fuse-integration-services-20-for-openshift/)

The example can be built and run on OpenShift using a single goal:

    mvn fabric8:deploy

When the example runs in OpenShift, you can use the OpenShift client tool to inspect the status

To list all the running pods:

    oc get pods

Then find the name of the pod that runs this quickstart, and output the logs from the running pods with:

    oc logs <name of pod>

You can also use the OpenShift [web console](https://docs.openshift.com/container-platform/3.3/getting_started/developers_console.html#developers-console-video) to manage the
running pods, and view logs and much more.

### Running via an S2I Application Template

Application templates allow you deploy applications to OpenShift by filling out a form in the OpenShift console that allows you to adjust deployment parameters.  This template uses an S2I source build so that it handle building and deploying the application for you.

First, import the Fuse image streams:

    oc create -f https://raw.githubusercontent.com/jboss-fuse/application-templates/GA/fis-image-streams.json

Then create the quickstart template:

    oc create -f https://raw.githubusercontent.com/jboss-fuse/application-templates/GA/quickstarts/spring-boot-camel-template.json

Now when you use "Add to Project" button in the OpenShift console, you should see a template for this quickstart. 

### Database
create table liquidacion ( Id_Sistema Varchar(1), Id_Usuar Varchar(12), Fecha_Lect Varchar(10), Nro_Fact Varchar(25), Tarifa Varchar(2), SubCatTar Varchar(1), TS Varchar(1), EBP Varchar(1), MAU Varchar(1), ELD Varchar(1), Tension Varchar(1), Tipo_Fact Varchar(1), Tipo_Lec Varchar(1), Tipo_Per Varchar(1), Periodo Varchar(2), Liquidacion Varchar(1), Nro_Fact_Orig Varchar(26), Per_Ref_Base Varchar(10), Cod_Exc_Base Varchar(1), Fecha_Emision Varchar(10), Fecha_Vto_1 Varchar(10), Fecha_Vto_2 Varchar(10), Cambio_Medidor Varchar(1), primary key(Id_Sistema, Id_Usuar, Fecha_Lect, Nro_Fact, Fecha_Emision) ) ENGINE=INNODB;

alter table liquidacion add column nada varchar(1);

create table energia ( Id_Sistema Varchar(1), Id_Usuar Varchar(12), Fecha_Lect Varchar(10), Nro_Fact Varchar(25), Fecha_Emision Varchar(10), Tipo_Energia Varchar(1), Tramo Varchar(1), Consumo double(10,3), Factor_Potencia double(9,3), nada Varchar(1) primary key (Id_Sistema, Id_Usuar, Fecha_Lect, Nro_Fact, Fecha_Emision,Tipo_Energia,Tramo) ) ENGINE=InnoDB;


Alter table energia add foreign key fk_liquidacion (Id_Sistema, Id_Usuar, Fecha_Lect, Nro_Fact, Fecha_Emision) references liquidacion (Id_Sistema, Id_Usuar, Fecha_Lect, Nro_Fact, Fecha_Emision) on delete no action on update cascade;Query OK, 0 rows affected (0.01 sec)               
Records: 0  Duplicates: 0  Warnings: 0

create table liquidacion ( Id_Sistema Varchar(1), Id_Usuar Varchar(12), Fecha_Lect Varchar(10), Nro_Fact Varchar(25), Tarifa Varchar(2), SubCatTar Varchar(1), TS Varchar(1), EBP Varchar(1), MAU Varchar(1), ELD Varchar(1), Tension Varchar(1), Tipo_Fact Varchar(1), Tipo_Lec Varchar(1), Tipo_Per Varchar(1), Periodo Varchar(2), Liquidacion Varchar(1), Nro_Fact_Orig Varchar(26), Per_Ref_Base Varchar(10), Cod_Exc_Base Varchar(1), Fecha_Emision Varchar(10), Fecha_Vto_1 Varchar(10), Fecha_Vto_2 Varchar(10), Cambio_Medidor Varchar(1), primary key(Id_Sistema, Id_Usuar, Fecha_Lect, Nro_Fact, Fecha_Emision) ) ENGINE=INNODB;

