`Sorenza Laplume`

# Compte rendu TP4

## Exercice 1. Gestion des utilisateurs et des groupes
### • Commencez par créer deux groupes groupe1 et groupe2

Pour créer les groupes j'utilise la commande suivante :
> sudo addgroup groupe1 pour créer le groupe1
>sudo addgroup groupe2 pour créer le groupe2

### • Créez ensuite 4 utilisateurs u1, u2, u3, u4 avec la commande useradd, en demandant la création de leur dossier personnel et avec bash pour shell

<pre>
 1 #!/bin/bash
  2
  3 sudo useradd -m u1
  4 sudo passwd u1
  5 sudo useradd -m u2
  6 sudo passwd u2
  7 sudo useradd -m u3
  8 sudo passwd u3
  9 sudo useradd -m u4
 10 sudo passwd u4
    
</pre>
Je vérifie que les utilisateurs sont créer dans /etc/passwd je remarque qu'il possède bien un dossier /home/u.1 à u4 à leur nom.
su
### • Placez les utilisateurs dans les groupes :
#### - u1, u2, u4 dans groupe1

Pour placer les utilisateurs précédant dans le groupe1 j'utilise la commande suivante :
>sudo usermod u1 -g groupe1
>sudo usermod u2 -g groupe1
>sudo usermod u4 -g groupe1

#### - u2, u3, u4 dans groupe2

Pour placer les utilisateurs précédant dans le groupe2 j'utilise la commande suivante :
>sudo usermod -a -G groupe2 u2
>sudo usermod u3 -g groupe2
>sudo usermod -a -G groupe2 u4

### • Donnez deux moyens d’afficher les membres du groupe2

Les deux moyens d'afficher les membres du groupe2 sont :
> members groupe2
> grep 'groupe2' /etc/group

### • Faites de groupe1 le groupe propriétaire de /home/u1 et /home/u2 et de groupe2 le groupe propriétaire de /home/u3 et /home/u4

Pour faire de groupe1 le groupe propriétaire de /home/u1 et /home/u2 j'utilise les commandes suivantes :
> chgrp groupe1 /home/u1
> chgrp groupe1 /home/u2

Pour que le groupe2 soit le groupe propriétaire de /home/u3 et /home/u4 j'utilise les commandes suivantes :
> chgrp groupe2 /home/u3
> chgrp groupe2 /home/u4

### • Remplacez le groupe primaire des utilisateurs :
#### - groupe1 pour u1 et u2

Pour remplacez le groupe primaire des utilisateurs u1 et u2 j'utilise :
>sudo usermod -a -G groupe1 u1
>sudo usermod -a -G groupe1 u2

#### - groupe2 pour u3 et u4

Pour remplacez le groupe primaire des utilisateurs u3 et u4 j'utilise :
>sudo usermod -a -G groupe2 u3
>sudo usermod -a -G groupe2 u4

### • Créez deux répertoires /home/groupe1 et /home/groupe2 pour le contenu commun aux groupes, et mettez en place les permissions permettant aux membres de chaque groupe d’écrire dans le dossier associé.

Pour créer les deux répertoires précédants je me place dans le répertoire /home.
J'utilise les commandes :
> sudo mkdir groupe1
> sudo mkdir groupe2

Pour permettre aux membre de chaque groupe d'écrire dans le dossier associé j'utilise les commandes :

> sudo chmod 511 groupe1
> sudo chmod 511 groupe2

### • Comment faire pour que, dans ces dossiers, seul le propriétaire d’un fichier ait le droit de renommer ou supprimer ce fichier ?

Dans ces dossiers pour que seul le propriétaire d'un fichier ait le droit de renommer ou de supprimer ce fichier il faut utiliser la commande **chmod 711** .

### • Pouvez-vous vous connecter en tant que u1 ? Pourquoi ?

Oui je peux me connecter en u1 car lors de la création je lui ai attribué un mot de passe.

### • Activez le compte de l’utilisateur u1 et vérifiez que vous pouvez désormais vous connecter avec son compte.
### • Quels sont l’uid et le gid de u1 ?

>uid=1001(u1) gid=1001(groupe1) groups=1001(groupe1)

### • Quel utilisateur a pour uid 1003 ?

L'utilisateur a pour uid 1003 est u3.

### • Quel est l’id du groupe groupe1 ?

L'id du groupe1 est 1001.

### • Quel groupe a pour guid 1002 ? ( Rien n’empêche d’avoir un groupe dont le nom serait 1002...)

C'est le groupe2 qui à pour guid 1002.

### • Retirez l’utilisateur u3 du groupe groupe2. Que se passe-t-il ? Expliquez.

Pour retirer l'utilisateur u3 du groupe groupe2 j'utilise la commande :

> sudo gpasswd -d u3 groupe2.

L'utilisateur u3 à pour groupe primaire groupe2 ont ne peut donc pas le supprimer de ce groupe.

### • Modifiez le compte de u4 de sorte que :

#### — il expire au 1er juin 2020

Pour que le compte u4 expire le 1er juin 2020 j'utilise la commande :
>sudo chage -E 2020-06-01 u4.

#### — il faut changer de mot de passe avant 90 jours

Pour que l'utilisateur change de mot de passe avant 90 jours j'utilise la commande :
>sudo chage -M 90 u4.

#### — il faut attendre 5 jours pour modifier un mot de passe

La commande qui doit faire que l'utilisateur doit attendre 5 jours pour modifier un mot de passe est :
>sudo chage -m 5

#### — l’utilisateur est averti 14 jours avant l’expiration de son mot de passe

La commande qui permet à l'utilisateur d'être averti 14 jours avant l'expiration de son mot de passe est :

> sudo chage -W 14

#### — le compte sera bloqué 30 jours après expiration du mot de passe

La commmande qui permet de bloqué le compte 3O jours après expiration du mot de passe est :
> chage -I u4

### • Quel est l’interpréteur de commandes (Shell) de l’utilisateur root ?

L'interpréteur de commandes de l'utilisateur root est : **"#"**.

### • à quoi correspond l’utilisateur nobody ?

L'utilisateur nobody est un utilisateur qui n'a aucun fichier lui appartenant et ne fait partit d'aucun groupe. Il possède les privilèges des "autres utilisateurs".

### • Par défaut, combien de temps la commande sudo conserve-t-elle votre mot de passe en mémoire ? Quelle commande permet de forcer sudo à oublier votre mot de passe ?

La commande sudo conserve le mot de passe en mémoire en 5min. 
La commande qui permet de forcer sudo à oublier le mot de passe est  **chage -E password**.



## Exercice 2. Gestion des permissions

### • Dans votre $HOME, créez un dossier test, et dans ce dossier un fichier fichier contenant quelqueslignes de texte. Quels sont les droits sur test et fichier ?

Les droits sur le dossier test sont : **wxr-wxr-x** ce qui veut dire que le propriétaire peut  écrire, exécuter et lire, le groupe peut écrire, exécuter et lire et les autres peuvent juste exécuter.

Les droits sur le fichier fichier sont : **-rw-rw-r** ce qui veut dire que le fichier est en lecture et écriture pour le propriétaire, lecture et écriture pour le groupe et lecture pour les autres. 

### • Retirez tous les droits sur ce fichier (même pour vous), puis essayez de le modifier et de l’afficher en tant que root. Conclusion ?

Je ne  peux pas afficher, écrire et lire le contenu de ce fichier, quand je suis connecté avec mon utilisateur. 
En tant que root je peux exécuter, écrire et lire le fichier.

### • Redonnez vous les droits en écriture et exécution sur fichier puis exécutez la commande echo "echo Hello" > fichier. On a vu lors des TP précédents que cette commande remplace le contenu d’un fichier s’il existe déjà. Que peut-on dire au sujet des droits ?

Nous n'avons pas la permission de lire ce fichier. Ce qui veut dire que l'on peut effectuer des modifications en écriture, exécuter le fichier mais pas lire son contenu.

### • Essayez d’exécuter le fichier. Est-ce que cela fonctionne ? Et avec sudo ? Expliquez.

Lorsque l'on essaye d'exécuter le fichier cela fonctionne.
Cependant avec sudo su nous pouvons lire le contenu du fichier.

### • Placez-vous dans le répertoire test, et retirez-vous le droit en lecture pour ce répertoire. Listez le contenu du répertoire, puis exécutez ou affichez le contenu du fichier fichier. Qu’en déduisez-vous ?Rétablissez le droit en lecture sur test

Nous n'avons plus la permission de voir ce que possède le répertoire test. Nous pouvons juste y entrer.

### • Créez dans test un fichier nouveau ainsi qu’un répertoire sstest. Retirez au fichier nouveau et au répertoire test le droit en écriture. Tentez de modifier le fichier nouveau. Rétablissez ensuite le droit en écriture au répertoire test. Tentez de modifier le fichier nouveau, puis de le supprimer. Que pouvezvous déduire de toutes ces manipulations ?

Le fichier est en "lecture seule", je peux modifier le fichier nouveau. Cependant pour l'enregistrer je dois utiliser la commande : **:wq!**.

Après modification le fichier reste en "lecture seule"  mais je peux toujours le modifier et l'enregistrer avec la commande **:wq!** et le lire.

Je peux supprimer le fichier nouveau.

### • Positionnez vous dans votre répertoire personnel, puis retirez le droit en exécution du répertoire test. Tentez de créer, supprimer, ou modifier un fichier dans le répertoire test, de vous y déplacer, d’en lister le contenu, etc…Qu’en déduisez vous quant au sens du droit en exécution pour les répertoires ?

Je ne peux pas faire toute les actions demandé en effet  la permission refusé. J'en déduit que le droit d'exécution permet d'ouvrir un répertoire ou un fichier.

### • Rétablissez le droit en exécution du répertoire test. Positionnez vous dans ce répertoire et retirez lui à nouveau le droit d’exécution. Essayez de créer, supprimer et modifier un fichier dans le répertoire test, de vous déplacer dans ssrep, de lister son contenu. Qu’en concluez-vous quant à l’influence des droits que l’on possède sur le répertoire courant ? Peut-on retourner dans le répertoire parent avec ”cd..” ? Pouvez-vous donner une explication ?

J'en conclue que les droits sur le répertoire parent son inférieur à ceux du groupe.
L'on peut retourner dans le répertoire parent avec "cd ..".

### • Rétablissez le droit en exécution du répertoire test. Attribuez au fichier fichier les droits suffisants pour qu’une autre personne de votre groupe puisse y accéder en lecture, mais pas en écriture.

Pour attribuer le droit en exécution du répertoire test j'utilise la commande : **chmod 711 test**.

Pour attribuer au fichier fichier les droits suffisant pour qu'une autre personne de mon groupe puisse y accéder en lecture mais pas en écriture j'utilise la commande : **chmod 751 fichier**.

### • Définissez un umask très restrictif qui interdit à quiconque à part vous l’accès en lecture ou en écriture, ainsi que la traversée de vos répertoires. Testez sur un nouveau fichier et un nouveau répertoire.

Pour un umask très restrictive j'utilise les commandes suivantes :
>umask 007
>umask -S
>touch nouveau_fichier
>umask g-rwx

### • Définissez un umask très permissif qui autorise tout le monde à lire vos fichiers et traverser vos répertoires, mais n’autorise que vous à écrire. Testez sur un nouveau fichier et un nouveau répertoire.

Pour un umask très permissif j'utilise les commandes suivantes:
> umask u+rwx
>umask g+rwx
>umask o+rwx
>touch nouveau_fichier2
>ll nouveau_fichier2 à les droit **rw-rw-rw-**


### • Définissez un umask équilibré qui vous autorise un accès complet et autorise un accès en lecture aux membres de votre groupe. Testez sur un nouveau fichier et un nouveau répertoire.

Pour un umask équilibré j'utilise les commandes suivantes :
>umask 133
>umask u+x
>touch nouveau_fichier3 
>>ll nouveau_fichier3 à les droit **rw-r-r-**

### • Transcrivez les commandes suivantes de la notation classique à la notation octale ou vice-versa (vous pourrez vous aider de la commande stat pour valider vos réponses) :

#### - chmod u=rx,g=wx,o=r fic

>chmod 534 fic

#### - chmod uo+w,g-rx fic en sachant que les droits initiaux de fic sont r--r-x---

>chmod 653 fic

#### - chmod 653 fic en sachant que les droits initiaux de fic sont 711

>chmod u+rx, g+rx, o+wx fic

#### - chmod u+x,g=w,o-r fic en sachant que les droits initiaux de fic sont r--r-x---

>chmod 124 fic

### • Affichez les droits sur le programme passwd. Que remarquez-vous ? En affichant les droits du fichier /etc/passwd, pouvez-vous justifier les permissions sur le programme passwd ?

Les droits du fichier passwd sont **-rw-r--r--**. Ce qui veux dire que le propriétaire peut lire et écricre, le groupe lire et les autres lire. Seul le propriétaire peut modifier le fichier passwd.
