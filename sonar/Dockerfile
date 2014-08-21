FROM	centos

MAINTAINER grzesiekw "g.wilkowicz@gmail.com"

RUN	yum install -y unzip tar

# Java

RUN     cd /tmp && \
        curl -b gpw_e24=http%3A%2F%2Fwww.oracle.com -b oraclelicense=accept-securebackup-cookie -O -L http://download.oracle.com/otn-pub/java/jdk/7u67-b01/jdk-7u67-linux-x64.tar.gz && \
        mkdir /usr/java && \
        tar -zxf /tmp/jdk-7u67-linux-x64.tar.gz -C /usr/java && \
        mv /usr/java/jdk1.7.0_67 /usr/java/jdk7 && \
        rm /tmp/jdk-7u67-linux-x64.tar.gz

ENV	PATH $PATH:/usr/java/jdk7/bin

# Sonar

RUN	cd /tmp && \
	curl -O -L http://dist.sonar.codehaus.org/sonarqube-4.4.zip && \
	unzip -d /opt /tmp/sonarqube-4.4.zip && \
	mv /opt/sonar* /opt/sonar

RUN	useradd sonar

RUN	sed -i s*sonar.jdbc.url=jdbc:h2:tcp://localhost:9092/sonar*sonar.jdbc.url=\${env:SONAR_JDBC_URL}*g /opt/sonar/conf/sonar.properties && \
	sed -i s*sonar.jdbc.username=sonar*sonar.jdbc.username=\${env:SONAR_DB_USERNAME}*g /opt/sonar/conf/sonar.properties && \
	sed -i s*sonar.jdbc.password=sonar*sonar.jdbc.password=\${env:SONAR_DB_PASSWORD}*g /opt/sonar/conf/sonar.properties && \
	sed -i s*#sonar.web.context=*sonar.web.context=\${env:SONAR_WEB_CONTEXT}*g /opt/sonar/conf/sonar.properties

RUN	chown -R sonar /opt/sonar

EXPOSE	9000

ENV	SONAR_JDBC_URL jdbc:h2:tcp://localhost:9092/sonar
ENV	SONAR_WEB_CONTEXT /

USER	sonar

CMD	/opt/sonar/bin/linux-x86-64/sonar.sh console


