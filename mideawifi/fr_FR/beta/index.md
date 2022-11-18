
# Plugin Mideawifi - BETA


![mideawifi_icon](https://user-images.githubusercontent.com/3704897/200172116-ac8de823-46a5-4ae3-9165-fbb591c640f7.png)


Mideawifi permet de contrôler et historiser les informations de climatiseurs construits par **[Midea](https://fr.wikipedia.org/wiki/Midea)** avec modules Wi-Fi. 
Si vous utilisez l'application smartphone **Nethome plus**, **Midea Air** ou **MSmartHome**, c'est probablement le constructeur Midea qui est derrière le contrôleur de climatiseur.  

Voici une liste non exhaustive de marques ayant parfois des contrôleurs électroniques Midea:  
- Altech  
- Carrier  
- Comfee&apos;  
- Inventor  
- Johnson   
- Midea  
- Pro Breeze    
- Qlima  
- Riello   

## Aperçu  
  
![image](https://user-images.githubusercontent.com/3704897/202679954-b5b8f481-eac5-4f97-9452-cbbe470074a9.png)  
  
# Dépendances  

La première étape est d'installer les dépendances. Le plugin mideawifi utilise un autre plugin, _Docker Management (docker2)_ qui est maintenu par Jeedom directement.  
![image](https://user-images.githubusercontent.com/3704897/200282392-7bdcd23b-a6ed-4113-81b3-40acf88448fb.png)  

# Configuration générale  

Une fois les dépendances installées, il faut saisir les identifiants de l'application Midea que vous utilisez.  
Le port n'est à changer que si vous utilisez déjà ce dernier.  
  
Sauvegardez puis appuyez sur "**Activation Docker**".  
L'action peut-être assez longue la première fois, dépendant de la puissance de votre machine (environ 5-10min sur un raspberry 3B+, sinon moins) car cela créé une image spécialement préparée pour être compatible avec votre système.  

Une fois que la première pastille docker est verte, vous pouvez appuyer sur le second bouton "**Démarrage du container Midea**"  

![image](https://user-images.githubusercontent.com/3704897/200291627-985b687d-b5ac-4335-b86d-f6cd4eef3c6f.png)  

C'est en principe plus rapide, moins d'une minute.  

Voilà le plugin est configuré pour communiquer avec l'univers PAC/clim/déshumidificateur de Midea!  
  
# Configuration d'un équipement  
  
Après avoir lancé l'ajout automatique, vous devriez retrouver tous les équipements liés à votre compte.  
  
![image](https://user-images.githubusercontent.com/3704897/201053367-b947704b-01d4-45a7-bb84-399283de13e8.png)  
  
En principe il n'y a rien à toucher à l'intérieur des équipements. (sauf le rendre visible, son objet parent et le catégoriser si vous souhaitez)  
  
![image](https://user-images.githubusercontent.com/3704897/201054699-05048f34-1d90-4212-9c16-ad753e70191b.png)  
  
*Précision importante:* si vous avez les anciens contrôleurs wifi OSK-102, qui ne sont pas "cloud only" vous n'aurez ni token, ni key, laissez les champs vides.  
  
# Scénarios  
  
  ![image](https://user-images.githubusercontent.com/3704897/202680751-883a360b-d988-4ed8-b846-cd2e35e4330b.png)  

  Niveau scénario, vous avez possibilité de mettre une température au 1/2 °C prêt. (alors que via le dashboard c'est au °C)  
  Note pour la vitesse de ventilation: 102 est la valeur pour que la ventilation soit automatique, sinon c'est entre 20 et 80. Le pas sera de 20 (pour respecter les paliers classiques: silencieux normal rapide etc...)  
  
# Scripts Tiers  
  
Mideawifi repose sur le script tiers npm **midea-beautiful-air** en version *v0.9.15*  
Vous pouvez trouver le code github original ici:  [nbogojevic/midea-beautiful-air](https://github.com/nbogojevic/midea-beautiful-air)  
  
# Informations complémentaires  
  
 - Le plugin n'a pas été testé avec tous les climatiseurs et avec toutes les configurations logicielles et réseaux.  
 Merci de faire un Issue sur [GitHub](https://github.com/ddelec24/mideawifi/issues) ou un message sur le forum [Community Jeedom](https://community.jeedom.com/) si jamais vous constatez un dysfonctionnement.  
  
## Aide - FAQ  
  
# La température est incorrecte  
Dans votre application aussi. Sur beaucoup de modèles les capteurs sont mal placés dans les unités.  
  
## Problèmes connus

- Le cloud midea n'est pas connu pour être très robuste. Si vous faites 5 commandes en moins d'une minute, il risque de ne pas apprécier et n'en faire que la moitié!  
- Actuellement il faut mettre les identifiants midea air / nethome plus. Il semblerait que Msmarthome ne soit pas totalement compatible.  

---------------------------------------------------------------
Pour toutes autres questions, merci de regarder si il n'y a pas déjà une réponse à votre interrogation, sinon demandez sur le [community jeedom](https://community.jeedom.com)
