# Plugin Signal

![image](https://user-images.githubusercontent.com/3704897/184921503-f55fe475-37ad-4830-a607-5a2cae63dd30.png)

## Présentation

Ce plugin a pour but de communiquer via la messagerie Signal.  
Vous pouvez ainsi recevoir des notifications directement sur votre smartphone équipé de l'application Signal. La récupération des messages est aussi activable (elle demande un peu plus de ressources, mais les tests sur un Raspberry pi3b+ montrent que c'est presque instantané).
  
    
## Prérequis

Même si c'est automatisé avec **Jeedom 4.2**, je précise que la connexion avec votre compte signal est isolée dans un container Docker, via le plugin *Docker Management* (plugin officiel de Jeedom). NodeJS est aussi installé en même temps que le plugin.

La première fois, il vous faudra votre ou vos smartphones pour une autorisation via QRCode.  
  
  
## Configuration

### Configuration générale

![image](https://user-images.githubusercontent.com/3704897/184922586-89fca769-efd7-41f5-b841-df79d5fe26ac.png)

Concernant les paramètres généraux, il n'y a en principe pas besoin de modifier les 3 premières informations.  
C'est seulement si vous avez déjà un service qui utilise ces mêmes ports ou que vous avez besoin de modifier le cycle de dialogue entre jeedom et le démon nodejs.  
**Au premier lancement** ou en cas de pastille rouge dans l'état du service API, cliquez sur  
![image](https://user-images.githubusercontent.com/3704897/184924283-2da5e6b6-92f9-4901-b1fc-2278188d6da0.png)


#### **Important**
La case permettant d'activer la réception des messages n'est visible qu'après avoir créé et associé votre premier téléphone. Si vous cochez cette case, vous devez **sauvegarder** la configuration bien entendu, mais vous devez aussi cliquer sur le bouton **Installation/Réinstallation du service** même si celui-ci était déjà installé et que vous aviez la pastille verte.

Vous pouvez ensuite redémarrer le démon si cela s'avère nécessaire.  
  
  
## Configuration des équipements
  
Maintenant que vous avez activé le service et qu'il est opérationnel dans la configuration générale, il vous faut associer votre premier appareil.  

![image](https://user-images.githubusercontent.com/3704897/184929561-3a924077-0913-45ae-b0d1-939eeebe483d.png)

Comme montré sur l'image ci-dessus, il faut saisir votre numéro au format international!
le plus simple est d'aller le récupérer sur votre téléphone, dans votre profil:  
/!\ Saisissez le sans les espaces!  

![image](https://user-images.githubusercontent.com/3704897/184930299-a86e686d-bbf9-4fdf-8896-71fc1de58185.png) 

**Enregistrez votre nouvel équipement**, puis cliquez sur le lien permettant l'association:  
![image](https://user-images.githubusercontent.com/3704897/184930054-aa347d98-1113-4c75-9bda-621228e30cb3.png)

Une page doit s'ouvrir avec un QRcode. Il est à usage unique et change à chaque fois. Prenez le smartphone ayant le numéro précédemment saisi puis dans le menu **Appareils reliés** => bouton [+] => Scannez. L'association est faite. Vous pouvez actualiser la page après quelques secondes, la pastille doit devenir verte.  

### Les commandes

![image](https://user-images.githubusercontent.com/3704897/184930963-63c30efc-27e0-4d57-b3e0-15211097f832.png)

- "Message reçu" correspond au message en lui-même. Ainsi vous pouvez utiliser cette commande pour déclencher des actions dans jeedom.  
- "Message brut reçu" existe car elle contient d'autres informations qui pourraient être interessantes dans des cas particuliers. Il y a les timestamps d'envoi par exemple. Information brute au encodé au format json.  
- "Envoi de message" permet d'envoyer un message simple.  
- "Envoi de fichier" permet aussi d'envoyer un message mais avec une pièce jointe. Les limitations sont à priori celles de signal (donc dépendant d'Android/iOS) mais au minimum 100Mo.   

Les messages reçus sont historisés 3 mois par défaut. Vous pouvez changer dans la configuration de la commande, bien évidemment.

## Utilisation sur le dashboard

![image](https://user-images.githubusercontent.com/3704897/184935108-e563830f-6ad3-4d0f-a7c6-6b516b5f1444.png)  

La tuile est toute simple car on est sur un plugin qui a surtout une utilité d'intéractions. On peut envoyer et recevoir un message (destinataire = expéditeur = numéro de l'équipement).  

## Utilisation en scénarios

Là où on peut avoir plus de possibilités, c'est bien dans les scénarios. Voici quelques exemples simples:  

![image](https://user-images.githubusercontent.com/3704897/184935002-5e0a489d-b5e0-4707-958f-73bc854d7f96.png)  

Sélectionnez la commande action qui va envoyer le message (et donc le numéro qui sera utilisé en tant qu'expéditeur), mettez votre message et le numéro qui doit recevoir le message (Attention il doit aussi exister dans le plugin et être actif!).  
  
Dans le cadre d'une pièce-jointe. vous pouvez utiliser une variable, un tag, une commande, peut importe. La valeur doit être soit un **lien internet** soit un **chemin local** (exemple: */home/jeedom/ma_video.mp4*)  
Dans ma capture, je recevrais un screenshot de ma caméra.  
  
  
En intéraction, on peut faire un systeme de Ask ou comme ceci:  
![image](https://user-images.githubusercontent.com/3704897/184937800-e43b6364-cf2b-4e0d-b34c-4b7d43de3283.png)  

Votre déclencheur sera là votre commande de message reçu. Vous pouvez répondre dans la foulée à votre smartphone!  


Voilà pour l'usage classique. On peut aller plus loin et bien sûr j'attends vos remontées si il y a des axes de développement ou améliorations.  

  
## Aide - FAQ

> Dans tous les cas, il faudra regarder au préalable les logs du plugin pour avoir plus d'informations. N'hésitez pas à mettre le mode debug il y aura pleins d'informations supplémentaires pour vous aider.  

- Je n'arrive pas à associer un nouvel équipement / le QRcode n'apparait pas il affiche une erreur.
- > Dans la configuration du plugin, il est impératif de désactiver la réception des messages, sauvegarder, puis appuyer sur le bouton pour réinstaller le service. Une fois en route, vous devriez pouvoir ajouter le nouveau numéro. Pensez ensuite à faire la marche inverse en recochant la réception une fois terminée! C'est une limitation dans le fonctionnement de l'API on est obligé faire comme çà.

- Pour toutes autres questions, merci de regarder si il n'y a pas déjà une réponse à votre interrogation, sinon demandez sur le [community jeedom](https://community.jeedom.com)
