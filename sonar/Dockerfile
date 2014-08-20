FROM centos

MAINTAINER grzesiekw "g.wilkowicz@gmail.com"

RUN yum install -y unzip tar

# Java

RUN     cd /tmp && \
        curl -b gpw_e24=http%3A%2F%2Fwww.oracle.com -b oraclelicense=accept-securebackup-cookie -O -L http://download.oracle.com/otn-pub/java/jdk/7u67-b01/jdk-7u67-linux-x64.tar.gz && \
        mkdir /usr/java && \
        tar -zxf /tmp/jdk-7u67-linux-x64.tar.gz -C /usr/java && \
        mv /usr/java/jdk1.7.0_67 /usr/java/jdk7 && \
        rm /tmp/jdk-7u67-linux-x64.tar.gz

ENV PATH $PATH:/usr/java/jdk7/bin

# Sonar

RUN	cd /tmp && \
	curl -O -L http://dist.sonar.codehaus.org/sonarqube-4.4.zip && \
	unzip -d /opt /tmp/sonarqube-4.4.zip && \
	useradd sonar

RUN	sed -i s*sonar.jdbc.url=jdbc:h2*#sonar.jdbc.url=jdbc:h2*g /opt/sonarqube-4.4/conf/sonar.properties && \
	sed -i s*#sonar.jdbc.url=jdbc:postgresql://localhost/sonar*sonar.jdbc.url=\${env:SONAR_DB_URL}*g /opt/sonarqube-4.4/conf/sonar.properties && \
	sed -i s*sonar.jdbc.username=sonar*sonar.jdbc.username=\${env:SONAR_DB_USERNAME}*g /opt/sonarqube-4.4/conf/sonar.properties && \
	sed -i s*sonar.jdbc.password=sonar*sonar.jdbc.password=\${env:SONAR_DB_PASSWORD}*g /opt/sonarqube-4.4/conf/sonar.properties

RUN	chown -R sonar /opt/sonarqube-4.4

USER	sonar

ENV	SONAR_DB_URL jdbc:h2:tcp://localhost:9092/sonar

CMD	/opt/sonarqube-4.4/bin/linux-x86-64/sonar.sh console


