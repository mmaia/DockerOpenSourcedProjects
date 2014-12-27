# run this with the following command, first build the image from this docker file using mysql v 5.6 from docker repo.
# docker build -t="mmaia/mysql:v1" .

FROM centos:centos6
MAINTAINER Marcos Maia "maia.marcos@gmail.com"

# make sure centos is up to date
RUN yum update -y && yum install tar -y

#copy files to tmp
COPY MySQL-server-5.6.22-1.linux_glibc2.5.x86_64.rpm tmp/MySQL-server-5.6.22-1.linux_glibc2.5.x86_64.rpm

# install mysql and start it
RUN cd tmp && chmod +x *.rpm && yum install MySQL-server-5.6.22-1.linux_glibc2.5.x86_64.rpm && service mysql start