TP 4 - Spéléologie réseau : descente dans les couches

Préparation d'une VM "patron"
Installation et configuration de la VM "patron" :
Installation de la VM patron comme éxigé par la sujet aucun problememe rencontré
grace au clonage de Virtual Box

1. Création des réseaux
on va avoir 2 réseau différent:
le 10.2.0.0 et le 10.1.0.0 avec un routeur qui servira de passerelle entre les
deux

2. Création des VMs
Simple clonage à partir de Virtual Box en attribuant les bonnes cartes réseaux
client  <--net1--> router <--net2--> server
Checklist sur les machines

Désactiver SELinux: déja fait
Installation de certains paquets réseau: déja fait
Désactivation de la carte NAT: déja fait

Définition des IPs statiques:
On vérifie la connection SSH pour voir si elle est fonctionnelle.Puis vous avez
vos trois fenêtres SSH ouvertes

Définition du nom de domaine
Remplissage du fichier /etc/hosts
client1 ping router1.tp4 sur l'IP 10.1.0.254
server1 ping router1.tp4 sur l'IP 10.2.0.254
Petit tableau récapitulatif :

Machine	net1	net2
client1.tp4	10.1.0.10	X
router1.tp4	10.1.0.254	10.2.0.254
server1.tp4	X	10.2.0.10

3. Mise en place du routage statique
Config route client 1 :
10.2.0.254 via 10.1.0.254
10.2.0.10 via 10.1.0.254

Config route client serveur 1 :
10.1.0.254 via 10.2.0.254
10.1.0.10 via 10.2.0.254

II. Spéléologie réseau
1. ARP
Le protocole ARP permet de connaître l'adresse MAC d'une machine quand on connaît
son IP.

La table ARP se remplit quand les VM comuniquent entre elle, tant qu'il n'y a pas
de communication la table ARP reste inchangé.

2. Wireshark
Wireshark permet d'analyser et de snifer les trames qui communique dans le
réseau, ici nous avons pour objectif  de comprendre ce qui se passe lorsque
l'on fait nos requete ARP.

A. Interception d'ARP et ping
Interception d'une requete arp et d'un ping on lance l'analyser. On lance un
ping, une requeter ARP et Wireshark s'occupe de les récupérer.

B. Interception d'une communication netcat
Identique que la requete ARP mais avec utilisation de netcat.
