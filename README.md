Referance --> https://thegeeksalive.com/how-to-install-sonarqube-on-centos/
Ubuntu: https://www.vultr.com/docs/how-to-install-sonarqube-on-ubuntu-16-04

Get jdk from official site
https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html
sudo yum install jdk-11.0.4_linux-x64_bin.rpm
Default jdk 11 installed path:  /usr/java/jdk-11.0.4/bin/java

Download the sonarqube from below link with LTS version is preferable:
https://www.sonarqube.org/downloads/
unzip sonarqube-developer-7.9.2.zip 
mv sonarqube-7.9.2/ sonarqube
Edit the Java 11 version path in below path
/usr/java/jdk-11.0.4/bin/java
vim sonarqube/conf/wrapper.conf 
chown <normal_user>. /opt/sonarqube -R

not required
<!---
vi /opt/sonarqube/conf/sonar.properties
Enter the database details as shown below.
sonar.jdbc.username=sonarqube_user
sonar.jdbc.password=password
sonar.jdbc.url=jdbc:mysql://localhost:3306/sonarqube_db?useUnicode=true&characterEncoding=utf8&rewriteBatchedStatements=true&useConfigs=maxPerformance

Open the SonarQube startup script and specify the sonarqube user details.
vi /opt/sonarqube/bin/linux-x86-64/sonar.sh
Add the following entry to it.
RUN_AS_USER=sonarqube
-->

/opt/sonarqube/bin/linux-x86-64/sonar.sh start


Ubuntu:
https://developerinsider.co/install-sonarqube-on-ubuntu/

RHEL/CentOS:
https://www.vultr.com/docs/how-to-install-sonarqube-on-centos-7
