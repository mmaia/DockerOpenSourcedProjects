# run this with the following command, first build the image from this docker file
# docker build -t="mmaia/wildfly:v1" .
#
# than run the image for the first time to random available ports on the host O.S
# docker run -i -t -P --name mmaia-wildfly mmaia/wildfly:v1 /opt/wildfly-8.2.0.Final/bin/standalone.sh -b 0.0.0.0 -bmanagement 0.0.0.0
# or run binding to specific defined ports on the host O.S(8080 and 9990)
# docker run -i -t -p 8080:8080 -p 9990:9990 --name mmaia-wildfly mmaia/wildfly:v1 /opt/wildfly-8.2.0.Final/bin/standalone.sh -b 0.0.0.0 -bmanagement 0.0.0.0
#
# after first run use start to run image again
# docker start mmaia-wildfly

FROM centos:centos6
MAINTAINER Marcos Maia "maia.marcos@gmail.com"

# make sure centos is up to date
RUN yum update -y && yum install tar -y

#create user and group to use with wildfly
RUN groupadd -r wildfly && useradd -r -g wildfly wildfly

#copy files to tmp
COPY wildfly-8.2.0.Final.tar.gz tmp/wildfly-8.2.0.Final.tar.gz
COPY jdk-7u71-linux-x64.tar.gz tmp/jdk-7u71-linux-x64.tar.gz

#extract files to opt/wildfly and opt/java that's where I like them to be
RUN cd tmp && gunzip wildfly-8.2.0.Final.tar.gz && gunzip jdk-7u71-linux-x64.tar.gz && tar -xf wildfly-8.2.0.Final.tar && tar -xf jdk-7u71-linux-x64.tar

#copy jdk and wildfly to /opt that's where I like them to be :) and delete original tar files from image
RUN cd tmp && mv jdk1.7.0_71 /opt && mv wildfly-8.2.0.Final /opt && rm -rf *.tar

#setup installed jdk to be default for image
RUN update-alternatives --install /usr/bin/java java /opt/jdk1.7.0_71/bin/java 1 \
&& update-alternatives --install /usr/bin/javac javac /opt/jdk1.7.0_71/bin/javac 1

#expose JBoss http and management ports from docker to host O.S
EXPOSE 8080 9990

#add user to manage wildfly
RUN /opt/wildfly-8.2.0.Final/bin/add-user.sh --silent=true admin admin

