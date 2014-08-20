FROM centos

MAINTAINER grzesiekw "g.wilkowicz@gmail.com"

RUN yum install -y tar

# Java

RUN	cd /tmp && \ 
	curl -b gpw_e24=http%3A%2F%2Fwww.oracle.com -b oraclelicense=accept-securebackup-cookie -O -L http://download.oracle.com/otn-pub/java/jdk/7u67-b01/jdk-7u67-linux-x64.tar.gz && \
	mkdir /usr/java && \
	tar -zxf /tmp/jdk-7u67-linux-x64.tar.gz -C /usr/java && \
	mv /usr/java/jdk1.7.0_67 /usr/java/jdk7 && \
	rm /tmp/jdk-7u67-linux-x64.tar.gz

ENV	PATH $PATH:/usr/java/jdk7/bin

# Nexus

RUN	cd /tmp && \
	curl -O -L http://www.sonatype.org/downloads/nexus-2.9.0-bundle.tar.gz && \
	tar -zxf nexus-2.9.0-bundle.tar.gz -C /opt && \
	mv /opt/nexus* /opt/nexus && \
	useradd nexus && \
	rm nexus-2.9.0-bundle.tar.gz

RUN     chown -R nexus /opt/sonatype-work && \
        chown -R nexus /opt/nexus

EXPOSE	8081

USER	nexus
	
CMD /opt/nexus/bin/nexus console
