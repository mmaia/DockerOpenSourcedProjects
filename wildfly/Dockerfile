FROM centos:centos6
MAINTAINER Marcos Maia "maia.marcos@gmail.com"

# make sure centos is up to date
RUN yum update -y && yum install tar -y

#create user and group to use with wildfly
RUN groupadd -r wildfly && useradd -r -g wildfly wildfly

#copy files to tmp
COPY wildfly-8.2.0.Final.tar.gz tmp/ && jdk-7u71-linux-x64.tar.gz tmp/

#extract files to opt/wildfly and opt/java that's where I like them to be :)
RUN cd tmp && gunzip wildfly-8.2.0.Final.tar.gz && gunzip jdk-7u71-linux-x64.tar.gz && tar -xf wildfly-8.2.0.Final.tar && tar -xv jdk-7u71-linux-x64.tar