---
layout: docs
title: Remote Access and Keys
description: Learn about SSH
group: tools
lang: fr
---

Secure Shell (SSH) est un programme informatique et un protocole de communication sécurisé permettant d'obtenir une communication où tous les segments TCP sont authentifiés et chiffrés.

L'authentification peut se faire soit avec un mot de passe, soit en utilisant la cryptographie asymétrique, ce qui évite la saisie d'un mot de passe. Dans ce cas, la clé publique est distribuée sur les systèmes sur lesquels on souhaite se connecter, alors que la clé privée (qu'on prendra le soin de protéger par un mot de passe) reste uniquement sur le poste à partir duquel on se connecte.


<a name="connect"></a>
## Connexion

Une connexion via nom d'utilisateur et mot de passe s'effectue de la manière suivante:

```bash
$ ssh username@host
```
	
Plutôt que d'utiliser l'authentification par mot de passe, il est possible d'utiliser une clé:

	$ ssh -i path_to_ssh_key username@host

Dans certains cas, il est nécessaire de renseigner le port sur le serveur distant:

	$ ssh username@host -p <port>


<a name="keys"></a>
## Gestion des clés

La liste des clés SSH d'un compte est située par défaut dans `~/.ssh/`:

	$ ls -l ~/.ssh

Par convention, le type de clé est précisé dans le nom (exemple: `my_key_rsa`) et la distinction clé publique / clé privée se fait en ajoutant le suffixe `.pub` au nom d'une clé publique.

Il existe généralement un couple de clés par défaut pour l'utilisateur, nommées `id_rsa` et `id_rsa.pub`. Il est toutefois possible et même recommandé de générer un nouveau couple de clés pour chaque service afin de bien les distinguer.

Il est également préférable de restreindre les droits sur une clé:

	$ chmod 400 path_to_ssh_key

Il est possible de configurer le fichier `~/.ssh/config` afin d'éviter de devoir saisir la commande de connexion en entier:

	Host <my_ssh_connection>
	HostName <host>
	User <username>
	IdentityFile <path_to_ssh_key>
 
Une connexion peut dès lors être établie de la sorte:

	$ ssh my_ssh_connection


### Génération de clés

Création d'une nouvelle clé SSH:

	$ ssh-keygen -t rsa -f my_key_rsa -C "email@example.com"

Il est fortement recommandé d'entrer une _passphrase_ afin de protéger l'utilisation de la clé. Pour éviter de devoir la saisir à chaque utilisation, il est possible de la stocker dans le Trousseau d'accès d'OS X via la commande `ssh-add -K path/to/my_key_rsa`.

Copie du contenu de la clé dans le presse-papier:

	$ pbcopy < my_key_rsa
	
Copie de la clé publique dans le répertoire `.ssh/authorized_keys` du serveur:

	$ scp my_key_rsa.pub username@host:.ssh/authorized_keys


### Accès au serveur

La liste des clés publiques autorisées à se connecter au serveur sont listées sur le serveur dans le fichier `/.ssh/authorized_keys`:

	$ mkdir .ssh
	$ chmod 700 .ssh
	$ cd .ssh
	$ touch authorized_keys
	$ chmod 600 authorized_keys
	$ cat ../my_key_rsa.pub >> authorized_keys
	$ rm ../my_key_rsa.pub

