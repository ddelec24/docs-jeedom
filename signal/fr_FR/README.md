# Plugin Signal

![image](https://user-images.githubusercontent.com/3704897/184921503-f55fe475-37ad-4830-a607-5a2cae63dd30.png)  

## Présentation

Ce plugin a pour but de communiquer via la messagerie Signal.  
Vous pouvez ainsi recevoir des notifications directement sur votre smartphone équipé de l'application Signal. La récupération des messages est aussi activable (elle demande un peu plus de ressources, mais les tests sur un Raspberry pi3b+ montrent que c'est presque instantané).
  
    
## Prérequis

Même si c'est automatisé avec **Jeedom 4.2**, je précise que la connexion avec votre compte signal est isolée dans un container Docker, via le plugin *Docker Management* (plugin officiel de Jeedom). NPM et NodeJS sont aussi installés en même temps que le plugin.

La première fois, il vous faudra votre ou vos smartphones pour une autorisation via QRCode.  
  
  
## Configuration

### Configuration générale

Il faut commencer par installer les dépendances.  

![image](https://user-images.githubusercontent.com/3704897/189480719-58cb838a-2fdf-49fd-9d23-9b3416b51627.png)  
  
Si vous voyez un encart rouge vous disant que *le service docker* n'est pas actif, c'est que le système n'a pas fini de s'initialiser. Merci de patienter et rafraichir la page jusqu'à ce qu'il disparaisse. Si il reste, pensez à **redémarrer votre machine**! Sinon merci de consulter la FAQ en bas de la documentation.  
  
Concernant les paramètres généraux, il n'y a en principe pas besoin de modifier les 3 premières informations.  
C'est seulement si vous avez déjà un service qui utilise ces mêmes ports ou que vous avez besoin de modifier le cycle de dialogue entre jeedom et le démon nodejs.  
**Au premier lancement** ou en cas de pastille rouge dans l'état du service API, cliquez sur  le bouton  
![image](https://user-images.githubusercontent.com/3704897/185181517-adb1a2e1-f720-4847-8409-b5b5908af0ca.png)  

  
## Configuration des équipements
  
Maintenant que vous avez activé le service et qu'il est opérationnel dans la configuration générale, il vous faut créer un nouvel équipement via "*Ajouter un numéro*" et associer votre appareil.  

![image](https://user-images.githubusercontent.com/3704897/189481045-8e24d32a-bad5-491a-9d22-42374ee1823e.png)  

Comme montré sur l'image ci-dessus, il faut saisir votre numéro au format international!
le plus simple est d'aller le récupérer sur votre téléphone, dans votre profil:  
/!\ Saisissez le sans les espaces!  

![image](https://user-images.githubusercontent.com/3704897/184930299-a86e686d-bbf9-4fdf-8896-71fc1de58185.png)  

**Enregistrez votre nouvel équipement**, puis cliquez sur le lien permettant l'association:  
![image](https://user-images.githubusercontent.com/3704897/189481067-57cce93e-4062-4d76-ad54-3e1fa56b6087.png)  

Une page doit s'ouvrir avec un QRcode. Il est à usage unique et change à chaque fois. Prenez le smartphone ayant le numéro précédemment saisi puis dans le menu **Appareils reliés** => bouton [+] => **Scannez** puis fermez la page avec le QRcode.  
L'association est faite. Vous pouvez actualiser la page de votre équipement après quelques secondes, la pastille doit devenir verte.  

### Les commandes

![image](https://user-images.githubusercontent.com/3704897/189669526-6e0d3d44-49c1-4b77-b53f-85e0c0f21207.png)    

- "Message reçu" correspond au message en lui-même. Ainsi vous pouvez utiliser cette commande pour déclencher des actions dans jeedom.  
- "Nom de l expéditeur" sera enregistré si disponible. Récupéré grâce à vos contacts signal.  
- "Numéro de l expéditeur" contient le numéro de l'expéditeur du message que vous venez de recevoir.  
- "Message brut reçu" existe car elle contient d'autres informations qui pourraient être interessantes dans des cas particuliers. Il y a les timestamps d'envoi par exemple. Information brute au encodée au format json.  
- "Envoi de message" permet d'envoyer un message simple.  
- "Envoi de fichier" permet aussi d'envoyer un message mais avec une pièce jointe. Les limitations sont à priori celles de signal (donc dépendant d'Android/iOS) mais au minimum 100Mo.   

Les messages reçus sont historisés 3 mois par défaut. Vous pouvez changer dans la configuration de la commande, bien évidemment.

## Activation de la réception

Comme on fait les choses dans l'ordre, on ne peut activer la réception dans jeedom qu'une fois qu'un numéro est associé.  
En revenant voir dans la configuration générale on aura une option permettant d'avoir cette fonctionnalité:  
  
![image](https://user-images.githubusercontent.com/3704897/185187801-8257f752-2815-4fc9-bff2-c511f52511a9.png)  

Après avoir coché la case, vous pourrez choisir le numéro à mettre en écoute dans jeedom pour les intéractions.  
Vous devez **sauvegarder** la configuration bien entendu, mais vous devez aussi cliquer de nouveau sur le bouton **Installation/Réinstallation du service** même si celui-ci était déjà installé et que vous aviez la pastille verte.  
  
Le démon devrait se relancer automatiquement.
  
## Utilisation sur le dashboard

![image](https://user-images.githubusercontent.com/3704897/189668206-131be4ec-779e-4cdf-8dfe-20f1d115134f.png)   

La tuile est toute simple car on est sur un plugin qui a surtout une utilité d'intéractions. On peut envoyer et recevoir un message (destinataire = expéditeur = numéro de l'équipement).  

## Utilisation en scénarios

Là où on peut avoir plus de possibilités, c'est bien dans les scénarios. Voici quelques exemples simples:  

![image](https://user-images.githubusercontent.com/3704897/185191241-bd9b8230-702c-431f-ab74-66cd14ffbb2e.png) 

Sélectionnez la commande action qui va envoyer le message (et donc le numéro qui sera utilisé en tant qu'expéditeur), mettez votre message et le numéro qui doit recevoir le message (Attention il doit aussi exister dans le plugin et être actif!).  
  
Dans le cadre d'une pièce-jointe. vous pouvez utiliser une variable, un tag, une commande, peut importe. La valeur doit être soit un **lien internet**, soit un **chemin local** (exemple: */home/jeedom/ma_video.mp4*)  
Dans ma capture ci-dessus, je recevrais un screenshot de ma caméra.  
  
  
En intéraction, on peut faire un système de Ask ou comme ceci:  
![image](https://user-images.githubusercontent.com/3704897/184937800-e43b6364-cf2b-4e0d-b34c-4b7d43de3283.png)  

Votre déclencheur sera là votre commande de message reçu. Vous pouvez répondre dans la foulée à votre smartphone!  


Voilà pour l'usage classique. On peut aller plus loin et bien sûr j'attends vos remontées si il y a des axes de développement ou améliorations.   
  
  
## Aide - FAQ  
  
Dans tous les cas, il faudra regarder au préalable les logs du plugin pour avoir plus d'informations. N'hésitez pas à mettre le mode debug il y aura pleins d'informations supplémentaires pour vous aider.  
  
  
- Je ne peux pas redémarrer le démon, est-ce normal?  
 > Il faut au préalable activer la réception des messages car il n'est nécessaire que dans ce cas précis. Inutile de faire tourner un démon inutilement.  
  
- Dois-je avoir un numéro signal dédié pour jeedom?  
 > C'est vous qui voyez. Sur votre smartphone vous pouvez intéragir en envoyant sur votre propre numéro. Signal vous dira "Note à mon intention" mais la communication se fait sans problème!  
  
- Je n'arrive pas à associer un nouvel équipement / le QRcode n'apparaît pas et affiche une erreur.  
 > Tout d'abord, il faut être en local pour effectuer la manipulation.  
 Ensuite dans la configuration du plugin, il est impératif de désactiver la réception des messages, de sauvegarder, puis d'appuyer sur le bouton pour réinstaller le service. Une fois en route avec la pastille verte, vous devriez pouvoir ajouter le nouveau numéro. Pensez ensuite à faire la marche inverse en recochant la réception, sauvegarder et de nouveau une réinstallation du service! C'est une limitation dans le fonctionnement de l'API, on est obligé faire comme ça.  
  
- J'ai un message m'indiquant *"Erreur d'exécution de la commande : sudo docker-compose -f /tmp/XXXXXXXX.yml up -d --force-recreate(1) => []"*. Que dois-je faire?  
 > Cela peut arriver la première fois. Le service docker met un certain temps à s'initialiser. Patientez 5 minutes puis retenter d'activer le service signal Api dans la page de configuration.  
  
- J'ai des erreurs (pas juste des warning qui sont normaux) lors de l'installation des dépendances, comment y remédier?  
 > Si vous aviez une ancienne installation docker, il se peut que cela pose problème. Si vous êtes sûr de ne pas utiliser docker, alors lancez en SSH la commande suivante qui va nettoyer proprement votre système de docker et ses dépendances:  
 ```bash  
  sudo apt remove -y docker-ce docker-ce-cli containerd.io && sudo apt purge -y docker-ce containerd.io && sudo apt autoremove -y && sudo apt clean && sudo apt autoclean  
 ```  
  Suite à ça, vous pouvez relancer les dépendances, attendre 5 minutes que tout se mette en place, et continuer l'installation du service Api.
  
## Problèmes connus

- Le nom des pièces jointes n'est pas personnalisable. Lorsqu'il s'agit d'un fichier qui n'est pas une image/vidéo et donc ne s'affiche pas directement dans la conversation, le nom sera une suite de caractères aléatoire. Le développeur à implanté la fonctionnalité de personnalisation il y a une dizaine de jours, j'attends qu'il mette ça en production !  

    ---------------------------------------------------------------
Pour toutes autres questions, merci de regarder si il n'y a pas déjà une réponse à votre interrogation, sinon demandez sur le [community jeedom](https://community.jeedom.com)
