Referance link:
https://www.fosstechnix.com/how-to-install-sonarqube-on-ubuntu-20-04/

sudo sysctl -w vm.max_map_count=262144
sudo sysctl -w fs.file-max=65536
ulimit -n 65536
ulimit -u 4096
vim /etc/security/limits.conf
sonarqube   -   nofile   65536
sonarqube   -   nproc    4096

sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get install wget unzip -y
sudo apt-get install openjdk-11-jdk -y
sudo apt-get install openjdk-11-jre -y
sudo update-alternatives --config java

java -version

Postgres installation
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -
sudo apt-get -y install postgresql postgresql-contrib
sudo systemctl start postgresql
pg_ctlcluster.
sudo systemctl enable postgresql
[sada@sada-ThinkPad-E14 (master)]$ sudo passwd postgres
New password:.
Retype new password:.
passwd: password updated successfully

[sada@sada-ThinkPad-E14 (master)]$ su - postgres
Password:.
postgres@ldap:~$ createuser sonar
postgres@ldap:~$ psql
psql (12.7 (Ubuntu 12.7-0ubuntu0.20.04.1))
Type "help" for help.

postgres=# ALTER USER sonar WITH ENCRYPTED password 'sonar';
ALTER ROLE
postgres=# CREATE DATABASE sonarqube OWNER sonar;
CREATE DATABASE
postgres=# grant all privileges on DATABASE sonarqube to sonar;
GRANT
postgres=# \q


Download and install sonarqube
sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.9.1.44547.zip
unzip sonarqube-8.9.1.44547.zip
mv sonarqube-8.9.1.44547 sonarqube
#sudo groupadd sonar
#sudo useradd -c "user to run SonarQube" -d /opt/sonarqube -g sonar sonar.
#sudo chown sonar:sonar /opt/sonarqube -R


Update database details and enable sonar database url
vim /opt/sonarqube/conf/sonar.properties.

sonar.jdbc.username=sonar
sonar.jdbc.password=sonar
sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube

vim /opt/sonarqube/bin/linux-x86-64/sonar.sh
update RUN_AS_USER=sada
/opt/sonarqube/bin/linux-x86-64/sonar.sh start
/opt/sonarqube/bin/linux-x86-64/sonar.sh status
tail -f /opt/sonarqube/logs/sonar.20210701.log

Got to browser:
http://localhost:9000/

Configure it as system user
sudo vim /etc/systemd/system/sonar.service
or copy sonar.service file present in repo to above path

sudo systemctl start sonar
sudo systemctl enable sonar
sudo systemctl status sonar

#To change port and access the sonarqube in other servers
vim /opt/sonarqube/conf/sonar.properties
sonar.web.host=0.0.0.0
sonar.web.port=9000

Manually run sonar project
mvn sonar:sonar -Dsonar.projectKey=sample -Dsonar.host.url=http://localhost:9000 -Dsonar.login=9cc4292533339e2047827f03921e159610099062

Access project -> http://localhost:9000
