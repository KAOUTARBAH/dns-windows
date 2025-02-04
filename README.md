# Installation et Configuration d'un Serveur DNS windows

## 1. Installation du Service DNS
- Ouvrir le gestionnaire de serveur sur le serveur Windows.
- Cliquer sur **Ajouter des rôles et fonctionnalités**.
- Dans l'assistant, cliquer sur **Suivant** jusqu'à la section **Sélection des rôles du serveur**.
- Cocher **Serveur DNS** puis cliquer sur **Suivant**.
- Suivre les étapes pour installer le rôle DNS.
- Une fois l’installation terminée, cliquer sur **Fermer**.

![serveur dns](https://github.com/KAOUTARBAH/dns-windows/blob/main/images/server-dns.png)

## 2. Configurer le Serveur DNS pour la Zone `rank.fr`
### Ouvrir la console DNS :
1. Accéder au menu **Démarrer**.
2. Chercher **DNS** et lancer la console **Gestionnaire DNS**.

### Créer une nouvelle zone de recherche directe :
1. Dans le **Gestionnaire DNS**, faire un clic droit sur **Zones de recherche directe** et sélectionner **Nouvelle zone**.
2. Choisir **Zone principale** et cliquer sur **Suivant**.
3. Nommer la zone `rank.fr`.
4. Sélectionner **Autoritaire pour cette zone** et cliquer sur **Suivant**.
5. Laisser les paramètres par défaut pour les fichiers de zone et cliquer sur **Suivant**.
6. Terminer la création de la zone.

![chemin adreese ip](https://github.com/KAOUTARBAH/dns-windows/blob/main/images/zone-rank.png)

## 3. Ajouter les Enregistrements A
### Ajouter un enregistrement A pour le serveur :
1. Clic droit sur la zone `rank.fr`, puis **Nouvel enregistrement d'hôte (A ou AAAA)**.
2. Dans **Nom d'hôte**, entrer un nom comme `Server-DHCP`.
3. Dans **Adresse IP**, entrer l’adresse IP statique du serveur DNS.
![chemin adreese ip](https://github.com/KAOUTARBAH/dns-windows/blob/main/images/chemin-add-ip.png)
4. Cliquer sur **Ajouter un hôte**.



### Ajouter un enregistrement A pour une machine avec réservation IP fixe :
1. Clic droit sur la zone `rank.fr`, puis **Nouvel enregistrement d'hôte (A ou AAAA)**.
2. Dans **Nom d'hôte**, entrer le nom de la machine, par exemple `Server-DHCP`.
3. Dans **Adresse IP**, entrer l'adresse IP réservée dans le serveur DHCP pour cette machine (`192.168.1.30`).
4. Cliquer sur **Ajouter un hôte**.

## 4. Ajouter un Enregistrement CNAME
### Ajouter un enregistrement CNAME pour le serveur :
1. Clic droit sur la zone `rank.fr`, puis **Nouvel enregistrement d’alias (CNAME)**.
2. Dans **Nom d'hôte**, entrer `dns`.
3. Dans **Nom canonique (FQDN)**, entrer le nom complet du serveur DNS (par exemple `Server-DHCP.rank.fr`).
4. Cliquer sur **OK** pour ajouter l’enregistrement CNAME.

## 5. Tests de Fonctionnement
### Test 1 : Résolution de nom depuis le serveur DNS
- Ouvrir une fenêtre **Invite de commandes** sur le serveur DNS.
- Utiliser la commande suivante pour tester la résolution de nom A :
  ```bash
  nslookup server-dhcp.rank.fr