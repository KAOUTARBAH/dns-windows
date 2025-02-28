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

![zone rank](https://github.com/KAOUTARBAH/dns-windows/blob/main/images/zone-rank.png)

## 3. Ajouter les Enregistrements A
### Ajouter un enregistrement A pour le serveur :
1. Clic droit sur la zone `rank.fr`, puis **Nouvel enregistrement d'hôte (A ou AAAA)**.
2. Dans **Nom d'hôte**, entrer un nom comme `Server-DHCP`.
3. Dans **Adresse IP**, entrer l’adresse IP statique du serveur DNS pour cette machine (`192.168.1.30`).
![Enregistrements-A](https://github.com/KAOUTARBAH/dns-windows/blob/main/images/Enregistrements-A.png)

4. Cliquer sur **Ajouter un hôte**.
![Enregistrements-A-ok](https://github.com/KAOUTARBAH/dns-windows/blob/main/images/Enregistrements-A-ok.png)

![Enregistrements-hote](https://github.com/KAOUTARBAH/dns-windows/blob/main/images/Enregistrements-hote.png)

## 4. Ajouter un Enregistrement CNAME
### Ajouter un enregistrement CNAME pour le serveur :
1. Clic droit sur la zone `rank.fr`, puis **Nouvel enregistrement d’alias (CNAME)**.
![CNAME](https://github.com/KAOUTARBAH/dns-windows/blob/main/images/CNAME.png)
2. Dans **Nom d'hôte**, entrer `dns`.
3. Dans **Nom canonique (FQDN)**, entrer le nom complet du serveur DNS (par exemple `Server-DHCP.rank.fr`).
![CNAME-conf](https://github.com/KAOUTARBAH/dns-windows/blob/main/images/CNAME-conf.png)
4. Cliquer sur **OK** pour ajouter l’enregistrement CNAME.
![CNAME-ok](https://github.com/KAOUTARBAH/dns-windows/blob/main/images/CNAME-ok.png)

## 5. Tests de Fonctionnement
### Test 1 : Résolution de nom depuis le serveur DNS
- Ouvrir une fenêtre **Invite de commandes** sur le serveur DNS.
- Utiliser la commande suivante pour tester la résolution de nom A :
  ```bash
  nslookup server-dhcp.rank.fr

- Tester également le CNAME :
  ```bash
   nslookup dns.rank.fr

![test-clt](https://github.com/KAOUTARBAH/dns-windows/blob/main/images/test-dns-server.png)

### Test 2 : Résolution de nom depuis la machine cliente
- Ouvrir une fenêtre **Invite de commandes** sur le serveur DNS.
- Utiliser la commande suivante pour tester la résolution de nom A :
  ```bash
  nslookup server-dhcp.rank.fr

- Tester également le CNAME :
  ```bash
  nslookup dns.rank.fr

![test-clt](https://github.com/KAOUTARBAH/dns-windows/blob/main/images/test-dns-clt.png)

### Test 3: Résolution inverse (facultatif)
- Si vous avez configuré la zone inverse, tester la résolution inverse sur le serveur ou la machine cliente :
  ```bash
  nslookup <adresse_IP_du_serveur>

![test-add](https://github.com/KAOUTARBAH/dns-windows/blob/main/images/test-ip-clt.png)


## 6. Configuration du Serveur DNS pour la Zone Inverse (Facultatif)
### Étapes pour configurer la résolution inverse (Reverse Lookup)

#### 1. Créer une nouvelle zone de recherche inverse
- Ouvrir la console **Gestionnaire DNS** , faire un clic droit sur **Zones de recherche inverse**, puis choisir l'option **Nouvelle zone**.
- Suivre l'assistant et choisir le bon sous-réseau pour la zone inverse.
- Valider pour créer la zone.
![Zone Inverse](https://github.com/KAOUTARBAH/dns-windows/blob/main/images/ZoneInverse.png)

#### 2. Ajouter un enregistrement PTR pour le serveur
- Dans la zone inverse, ajouter un enregistrement PTR pour l'adresse IP du serveur.
- Ce PTR doit pointer vers le nom suivant : `server-dhcp.rank.fr`.
- Enregistrer les modifications.
![Zone Inverse ok](https://github.com/KAOUTARBAH/dns-windows/blob/main/images/Zone-Inverse-ok.png)





