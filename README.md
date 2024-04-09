# parchado-was-ihs-plg
En esta sección se brindará los comandos de manera genérica para poder parchar un WAS, IHS y PLG.

Aplicar fix a los servidores (WAS - IHS) nueva granja

1. PREREQUISITO______________________________________________________________________________________
IMPORTANTE :  
○ Bajar los servicios WAS o IHS del server a intervenir

○ Ingresar por ssh a cada uno e ingresar el siguiente comando

ps -ef | grep java 
kill -9 PID con el wasadmin (de preferencia siempre levantarlo con el wasadmin)
○ Sacar un backup config del was

cd /opt/IBM/WebSphere/AppServer/profiles/IMOVIL_CERT/bin
./backupConfig.sh

2. PROCEDIMIENTO____________________________________________________________________________________

· WAS
/opt/IBM/InstallationManager/eclipse/tools/imcl install com.ibm.websphere.ND. v90_9.0.5018.20231113_1345 -repositories /opt/IBM/WebSphere/FIX90518/repository.config -silent -acceptLicense -sP
 
· IHS 
/opt/IBM/InstallationManager/eclipse/tools/./imcl install com.ibm.websphere.IHS.v90_9.0.5018.20231113_1345-repositories /opt/IBM/WebSphere/FIX90518/repository.config -installationDirectory /opt/IBM/HTTPServer -acceptLicense -properties  user.ihs.httpPort=80 -sP

· PLG
/opt/IBM/InstallationManager/eclipse/tools/./imcl install com.ibm.websphere.PLG.v90_9.0.5018.20231113_1345 -repositories /opt/IBM/WebSphere/FIX90518/repository.config -installationDirectory /opt/IBM/WebSphere/Plugins -acceptLicense -sP
 
○ Iniciar los servicios WAS e IHS 
· WAS (con el usuario wasadmin)
/opt/IBM/WebSphere/AppServer/profiles/IMOVIL_CERT/bin/startNode.sh
/opt/IBM/WebSphere/AppServer/profiles/IMOVIL_CERT/bin/startServer.sh IMOVIL_CERTX

· IHS (puede ser con root)
/opt/IBM/HTTPServer/bin/apachectl start
/opt/IBM/HTTPServer/bin/adminctl start

Terminado.

