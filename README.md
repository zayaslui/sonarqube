--instalar postgres
````
sudo passwd postgres
su postgres
createuser sonar
psql
ALTER USER sonar WITH ENCRYPTED PASSWORD 'sonarqube';
CREATE DATABASE sonarqube OWNER sonar;
GRANT ALL PRIVILEGES ON DATABASE sonarqube to sonar;
\q
sudo systemctl restart postgresql
sudo systemctl status -l postgresql
sudo netstat -tulpena | grep postgres
````

descargar binario
sudo curl -O https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.3.0.34182.zip

````
linux
mover a /opt
crear grupo sonar
sudo groupadd sonar
asignar como propietario de la carpeta sonar
sudo useradd -c "SonarQube - User" -d /opt/sonarqube/ -g sonar sonar
sudo chown sonar:sonar /opt/sonarqube-8.3.0.34182/ -R

//configurar sonar

error incrementar vm.max_map_count
# echo "vm.max_map_count=262144" >> /etc/sysctl.conf


#firewall
sudo ufw allow 9000,9001/tcp

#descargar el sonar scanner cli

sudo wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.2.0.1227-linux.zip

modificar el /conf/sonar-scanner.properties para configurar el host del servidor si tenemos otra parte


#convertir el sonar-scanner en ejecutable 
sudo chmod +x sonar-scanner-3.2.0.1227-linux/bin/sonar-scanner
#para ejecutar desde cualquier parte del servidor sin saber exactamente el nombre de la ruta creamos un link simbolico
sudo ln -s /opt/sonarscanner/sonar-scanner-3.2.0.1227-linux/bin/sonar-scanner /usr/local/bin/sonar-scanner

#descargamos test de github

#test
sonar-scanner -D sonar.login=mitoken[desde usuario generar token]

#definiciones
DEUDA TECNICA
Principales indicadores: fiabilidad, la seguridad y la mantenibilidad

Compuerta de Calidad:  filtro de politicas de calidad de la empresa.

Mantener nuevo codigo

#Integracion de SonarScanner con Apache Ant

sudo wget https://binaries.sonarsource.com/Distribution/sonarqube-ant-task/sonarqube-ant-task-2.7.0.1612.jar

sudo mkdir /opt/sonarscanner/sonar-scanner-ant
sudo mv sonarqube-ant-task-2.7.0.1612.jar /opt/sonarscanner/sonar-scanner-ant/























=======
````
>>>>>>> ace49181b9967dfadc5f12da80f6f61468645fd8
