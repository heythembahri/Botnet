# Botnet
#Botnet

-Un botnet est un réseau d’ordinateurs capables de recevoir des commandes à distance et de les exécuter localement. Ils sont généralement utilisés pour diverses activités malveillantes, notamment les attaques par déni de service distribué (DDoS) ou la distribution massive de logiciels espions.
Parmi les botnets les plus connus figurent Mirai et Gameover Zeus, qui contrôlent respectivement 3800 et 3.6 millions d’appareils connectés à Internet.  

**DDos :** Distributed Denial of Service, est une attaque informatique visant à rendre un site web indisponible en inondant ses serveurs par une grande quantité de requetes au point qu’il ne puisse plus répondre aux utilisateurs légitimes.
**Il existe plusieurs types d’attaque DDoS** 
• <u>Attaques par saturation de bande passante :<u> consommation de la bande passante réseau disponible du serveur cible, le rendant inaccessible

• <u>Attaques par saturation de ressources serveur :<u> ciblent les ressources du serveur, comme le processeur ou la mémoire, pour épuiser ses capacités.

• <u>Attaques au niveau applicatif :<u> visent directement les applications ou services spécifiques d'un site web (une attaque HTTP flood), en envoyant des requêtes complexes qui consomment beaucoup de ressources.

**Pour construire un botnet avec succés il faut intégrer :**
-Un nœud maitre : celui qui contrôle tous les autres nœuds.
-Déploiement des malwares déguisés sur les ordinateurs ciblés (nœuds esclaves).
-Transmission de commande depuis le nœud maitre vers les nœuds esclaves.

##Initialisation du code : 
![image](https://github.com/user-attachments/assets/3ea94242-116c-4bec-b423-be2b4da9a042)
1.	Ouverture de fichier bot.c et récupération du nom de l’utilisateur de l’ordinateur et le stocker dans une variable. 
2.	Connexion au maitre après avoir son adresse IP et le numèro de port. (localhost 127.0.0.1) et (port9 9999 pour les tests locaux)
3.	Initialisation du canal de communication (socket) par la fonction init_channel() (adresse IP, port, nom)

##Définition de la fonction :
-La fonction init_channel () est responsable de l’établissement de la connexion réseau entre l’esclave et le maitre

-Definition d’une variable « msg » pour stocker les messages envoyés.
-Une structure sockaddr_in appelée server est utilisée pour stocker les informations sur le serveur (adresse IP, domaine de communication, et numéro de port).
-Configuration de l’adresse IP en utilisant la fonction **inet_addr ()** (convertir en format binaire).
-Domaine de communication definit sur **AF_INET**.
-Le port est converti en « network byte order » à l’aide de la fonction **htons() **
**Le "network byte order" désigne l'ordre des octets utilisé pour transmettre les données sur un réseau.
![image](https://github.com/user-attachments/assets/15596c3f-3111-46c5-94d1-38ccd5d70561)
**-Création d’un socket** pour assurer la communication réseau et la stocker dans la variable channel, si ma création échoue, cela retourne une valeur négative et le programme se termine avec un message d’erreur.
**-Connect()** est designé pour etablir la connexion entre le client et le serveur (escalve et maitre).
![image](https://github.com/user-attachments/assets/76f10ac9-bd1c-4e5e-b26b-cb400fb97ac0)
**-Boucle Infinie :** Une boucle infinie (while(1)) est utilisée pour écouter en continu les messages venant du master. Elle assure que le programme reste actif et prêt à recevoir des instructions à tout moment.
**Receive() :** Cette fonction est appelée pour recevoir les données envoyées par le master via le socket. 
**Parse() :** Après avoir reçu un message, cette fonction est appelée pour analyser le contenu du message reçu.
![image](https://github.com/user-attachments/assets/adece4bc-3e0e-4769-b63d-f9f5c239edff)

-Vérifier si le message est bien ciblé.
![image](https://github.com/user-attachments/assets/238a3e31-8f8d-4f30-8a77-ced7aec64571)


-La fonction execute() exécute la commande reçue en l'envoyant à la ligne de commande, puis envoie la sortie de la commande au maître.
**Compilation :** 
![image](https://github.com/user-attachments/assets/1d00e074-db3b-4de9-8a7b-8349ae9137c9)
Cela compile les fichiers source et génère un exécutable appelé slave dans le répertoire bin.

##Déguiser le malware : 
-Il est possible de masquer un logiciel malveillant en le présentant comme une image, par exemple, une image d'un panda. Cela permet de tromper l'utilisateur en lui faisant croire qu'il ouvre simplement une image, alors qu'en réalité, il exécute un logiciel malveillant.
##Comment améliorer la robustesse du botnet ?
###Les extensions : 
**Achieve Persistence :** Cette extension vise à garantir que le malware reste actif même après un redémarrage de l'ordinateur. Les botnets peuvent devenir des sources fiables d'activité malveillante s'ils peuvent redémarrer automatiquement
**Peer-to-Peer Network :** Un réseau P2P (peer-to-peer) permet à chaque nœud de communiquer directement avec d'autres nœuds sans passer par un serveur central. Cela renforce la résilience du botnet, car il n'y a pas de point unique de défaillance.
**Add in Several Levels of Misdirection : ** La structure maître-esclave actuelle présente des vulnérabilités, car la désactivation du maître libère tous les esclaves, on peut ajouter des couces en rendant le chemin des commandes plus compliqué..

