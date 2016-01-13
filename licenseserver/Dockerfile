FROM centos:7
MAINTAINER Karel Van Roey <info at 3wh.be>

ENV ip_addr 10.1.1.1
ENV licenseserver_binary licenseserver_10.11.0_LINUX_X86_64.zip

RUN yum -y update && yum -y install net-tools vim unzip && yum clean all
RUN mkdir /components

COPY $licenseserver_binary /components/
RUN unzip /components/$licenseserver_binary -d /components/licenseserver
COPY licensekey.dat /components/licenseserver/

RUN echo $'ifconfig eth0:1 $ip_addr netmask 255.255.255.0 up\n\
cd /components/licenseserver\n\
./licenseserver.exe\n\
cd / \n'\
>> /start.sh
RUN chmod +x /start.sh

EXPOSE 20000

ENTRYPOINT [ "nohup", "./start.sh", "&" ]
