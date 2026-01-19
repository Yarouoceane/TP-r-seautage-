PROJET DE MISE EN PLACE D'UNE INFRASTRUCTURE RÉSEAU POUR UN ÉTABLISSEMENT UNIVERSITAIRE
OBJECTIFS DU TRAVAIL
Objectif Principal
Concevoir et déployer une infrastructure réseau complète pour un établissement universitaire réparti en trois zones fonctionnelles distinctes, permettant une communication sécurisée et efficace entre tous les services.
Objectifs Spécifiques
1.	Segmentation logique : Créer trois zones réseau indépendantes (Classes, Administrative, Logements) avec isolation des flux
2.	Hiérarchisation réseau : Implémenter une architecture à trois couches (accès, distribution, cœur)
3.	Gestion d'adressage : Mettre en place un plan d'adressage IP cohérent et scalable
4.	Connectivité contrôlée : Permettre la communication interzone tout en maintenant leur indépendance
5.	Redondance et fiabilité : Concevoir une architecture tolérante aux pannes
6.	Gestion centralisée : Implémenter des services réseau centraux (DHCP, DNS)
TECHNOLOGIES UTILISÉES
Équipements Réseau
•	Routeurs Cisco 2911 : Pour le routage interzones et inter-étages
•	Switchs Multilayer Cisco 3560 : Pour le cœur de réseau et la distribution
•	Switchs d'accès Cisco 2960 : Pour la connectivité des postes utilisateurs
•	Serveurs : Pour les services DHCP et DNS
Protocoles et Technologies
•	Routage statique : Pour la gestion des routes entre zones
•	VLANs : Pour la segmentation logique (optionnel selon configuration)
•	Spanning Tree Protocol (STP) : Pour éviter les boucles dans le réseau
•	DHCP : Attribution automatique d'adresses IP
•	DNS : Résolution de noms de domaine
•	Sous-réseaux VLSM : Utilisation efficace de l'espace d'adressage
Logiciels
•	Cisco Packet Tracer 8.x : Pour la simulation et le test de l'architecture
•	IOS Cisco : Système d'exploitation des équipements réseau
INSTRUCTIONS POUR EXÉCUTER LE PROJET
Prérequis
1.	Matériel logiciel :
o	Cisco Packet Tracer installé (version 8.0 ou supérieure)
o	Fichier de projet fourni (.pkt)
2.	Connaissances requises :
o	Bases de l'adressage IP et des sous-réseaux
o	Notions de routage et de commutation
o	Familiarité avec l'interface CLI de Cisco
Étapes d'Exécution
Étape 1 : Préparation de l'environnement
1.	Ouvrir Cisco Packet Tracer
2.	Charger le fichier de topologie fourni
3.	Vérifier que tous les équipements sont présents :
o	1 Routeur principal
o	1 Switch cœur multilayer
o	3 Switchs multilayer de zone
o	12 Routeurs d'étages
o	12 Switchs d'accès
o	24 PCs
o	2 Serveurs
Étape 2 : Configuration des équipements
Ordre recommandé de configuration :
1.	Routeur Principal :
text
enable
configure terminal
hostname R-PRINCIPAL
interface gigabitEthernet 0/0
ip address 10.0.0.1 255.255.255.252
no shutdown
exit
2.	Switch Cœur :
text
enable
configure terminal
hostname SW-COEUR
interface vlan 1
ip address 10.0.0.2 255.255.255.252
no shutdown
exit
3.	Switchs Multilayer de zones (répéter pour Classes, Admin, Logements) :
text
enable
configure terminal
hostname SW-CLASSES
interface fastEthernet 0/5
no switchport
ip address 10.0.1.2 255.255.255.252
no shutdown
exit
4.	Routeurs d'étages (configurer selon le plan d'adressage) :
text
enable
configure terminal
hostname R-B1-E1-CLASSES
interface gigabitEthernet 0/1
ip address 192.168.100.1 255.255.255.252
no shutdown
exit
interface gigabitEthernet 0/0
ip address 192.168.10.1 255.255.255.0
no shutdown
exit
ip route 0.0.0.0 0.0.0.0 192.168.100.2
end
copy running-config startup-config
5.	Serveurs :
o	Serveur DHCP : Configurer les pools pour chaque réseau
o	Serveur DNS : Définir l'adresse 192.168.99.11
6.	PCs :
o	Attribuer les IPs statiques selon le plan
o	Vérifier les passerelles et DNS
Étape 3 : Configuration du routage
1.	Sur le Routeur Principal, ajouter les routes statiques :
text
configure terminal
ip route 192.168.10.0 255.255.255.0 10.0.1.2
ip route 192.168.11.0 255.255.255.0 10.0.1.2
... (pour tous les réseaux)
end
2.	Sur chaque Switch Multilayer, ajouter la route par défaut :
text
ip route 0.0.0.0 0.0.0.0 [IP_du_switch_coeur]
Étape 4 : Tests de validation
Séquence de tests recommandée :
1.	Test de base :
text
Sur chaque PC : ping [passerelle_locale]
Exemple : ping 192.168.10.1
2.	Test intra-zone :
text
PC Zone Classes Etage 1 : ping 192.168.11.10
3.	Test inter-zones :
text
PC Zone Classes : ping 192.168.20.10
4.	Test des services :
text
ping 192.168.99.10  (serveur DHCP)
ping 192.168.99.11  (serveur DNS)
Étape 5 : Vérifications finales
1.	Vérifier la table de routage sur chaque équipement :
text
show ip route
2.	Vérifier l'état des interfaces :
text
show ip interface brief
3.	Vérifier la configuration courante :
text
show running-config
Dépannage Rapide
•	Si un ping échoue, vérifier dans l'ordre :
1.	Câblage et état des interfaces (no shutdown)
2.	Adresses IP et masques de sous-réseau
3.	Routes dans les tables de routage
4.	ACLs ou filtres éventuels
Sauvegarde des Configurations
Après chaque configuration réussie :
text
copy running-config startup-config
Remarques Importantes
1.	Temps de convergence : Attendre 30-60 secondes après les modifications
2.	Ordre de configuration : Respecter l'ordre hiérarchique (cœur → distribution → accès)
3.	Documentation : Noter toutes les adresses IP attribuées
4.	Tests incrémentiels : Tester après chaque étape de configuration
Ce projet démontre une architecture réseau d'entreprise typique, scalable et maintenable, répondant aux besoins d'un établissement universitaire moderne.

# TP-r-seautage-
