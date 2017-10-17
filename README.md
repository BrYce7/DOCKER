# Projet Docket Tomcat & Postgresql

# Le projet était de créer un serveur Tomcat et de le lier à une base de données Postgresql.

Pour cela nous avons crée 2 containers, chacun montés sur 2 images en Dockerfile.

Le container de Tomcat est monté sur le Dockerfile du dossier warrepo, on a utilisé l'image officielle tomcat:8-jre8 et on copie le dossier donné par notre professeur dbproject.war (qui contient le contenu du site) dans le dossier /usr/local/tomcat/webapps/ pour que le serveur tomcat puisse décompresser le dossier et le lancer.

Le container de Posgresql est monté sur l'image de postgres:9.5, ici aussi, on copie la base de donnée créée par le professeur pour réutiliser sa structure. On utilise également VOLUME pour enregistrer et faire persister les données même si le container est stoppé.

Une fois les 2 Dockerfile crées on va build les images dessus grâce à la commande "docker build -t myname ."

Une fois les 2 images créees ont peut run les 2 containers grace aux commandes:

+ docker run -d --name db -v /bddData:/var/lib/postgresql/data nomDeMonImagePostgresql

+ docker run -d --name MyApp -p 8888:8080 --link db nomDeMonImageTomcat

le -d permet de lancer le container en deamon (en tache de fond), on lui donne un nom grâce à --name, l'option -p permet de lui donner un port (ici le port 8888), l'option -v quant-à elle permet de lier un dossier en local avec un dossier du container pour la persistence des données. Enfin on utilise --link db pour lier le container tomcat au container postgresql. On lui indique ensuite de nom de l'image préalablement crée pour monter le container dessus.

Une fois les 2 containers lancés, on peut accéder a l'application web et avoir une base de données persistente derrière.






