FROM centos:7
MAINTAINER Karel Van Roey <info at 3wh.be>

ENV ip_addr 10.1.1.1
ENV licenseserver_binary licenseserver_10.11.0_LINUX_X86_64.zip

RUN yum -y update && yum -y install net-tools vim unzip && yum clean all
# route add -host $ip_addr dev lo -- does not work, disallowed by docker
RUN ifconfig eth0:1 $ip_addr netmask 255.255.255.0 up # requires docker to start with "--cap-add=NET_ADMIN" or "--privileged"
RUN mkdir /components

COPY $licenseserver_binary /components/
RUN unzip $licenseserver_binary -d /components/licenseserver
COPY licensekey.dat /components/licenseserver/

CMD [ "nohup", "/components/licenseserver/licenseserver.exe", "&" ]
