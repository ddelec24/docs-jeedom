
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
  
![image](https://user-images.githubusercontent.com/3704897/204097207-b6488326-d70c-48b8-ab2c-57c076780517.png)  
  
# Point d'attention  
/!\ Vos appareils (splits, déshumidificateurs) ont une adresse IP, qui sert à communiquer sur le réseau. Il faut fixer l'adresse IP sur votre routeur en mettant un bail permanent. Si vous avez besoin d'aide sur le sujet, n'hésitez pas à chercher sur le forum.  

# Dépendances  

La première étape est d'installer les dépendances. Le plugin mideawifi utilise un autre plugin, _Docker Management (docker2)_ qui est maintenu par Jeedom directement.  
![image](https://user-images.githubusercontent.com/3704897/200282392-7bdcd23b-a6ed-4113-81b3-40acf88448fb.png)  

# Configuration générale  

Une fois les dépendances installées, il faut saisir les identifiants de l'application Midea que vous utilisez.  
**[Expérimental]** Si vous êtes dans l'obligation d'utiliser l'application MsmartHome, cochez la case correspondante pour voir si la découverte des appareils fonctionne (et me contacter si besoin)  
Choisissez la fréquence de récupération des informations sur vos appareils. (5 minutes par défaut)  
Le port n'est à changer que si vous utilisez déjà ce dernier.  
  
Sauvegardez puis appuyez sur "**Activation Docker**".  
L'action peut-être assez longue la première fois, dépendant de la puissance de votre machine (environ 5-10min sur un raspberry 3B+, sinon moins) car cela créé une image spécialement préparée pour être compatible avec votre système.  

Une fois que la première pastille docker est verte, vous pouvez appuyer sur le second bouton "**Démarrage du container Midea**"  
  
![image](https://user-images.githubusercontent.com/3704897/211515013-eb1ddbb5-6a4f-4497-a2cd-cee47a38725e.png)  
  
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

  Niveau scénario, vous avez possibilité de mettre une température au ½ °C près. (alors que via le dashboard c'est au °C)  
  Note pour la vitesse de ventilation: 102 est la valeur pour que la ventilation soit automatique, sinon c'est entre 20 et 80. Le pas sera de 20 (pour respecter les paliers classiques: silencieux normal rapide etc...)  
  
  Notez que l'on peut passer une série de commandes en bloc code (cela évite d'avoir un bug du cloud quand on envoi trop d'ordres d'un coup)  
  La commande action se nomme "*Commandes personnalisées*". Voici commment procéder:  
  
  ```php
  // mettez l'équipement qui vous correspond
  $equipement = "#[test][Clim Salon][Commandes personnalisées]#";
  // voir doc en dessous pour la liste des possibilités
  $mesCommandes = "--running 1 --fan-speed 60";
  
  // laissez comme ça
  $sendCmd = cmd::byString($equipement);
  $sendCmd->execute(array('text' => $mesCommandes));
  ```
  
  Voici la liste de toutes les commandes possibles:  
  ```markdown
  --beep-prompt BEEP_PROMPT
                        turn beep prompt on/off (dehumidifier, air conditioner)
  --fan-speed FAN_SPEED
                        Current fan speed (dehumidifier, air conditioner)
  --ion-mode ION_MODE   ion (anion) mode on/off (dehumidifier)
  --mode MODE           operating mode (dehumidifier, air conditioner)
  --pump PUMP           water pump on/off (dehumidifier)
  --pump-switch-flag PUMP_SWITCH_FLAG
                        Pump switch flag - Disables pump (dehumidifier)
  --running RUNNING     turn on/off (dehumidifier, air conditioner)
  --sleep-mode SLEEP_MODE
                        sleep mode on/off (dehumidifier)
  --target-humidity TARGET_HUMIDITY
                        Target humidity (dehumidifier)
  --vertical-swing VERTICAL_SWING
                        vertical swing mode on/off (dehumidifier, air conditioner)
  --comfort-sleep COMFORT_SLEEP
                        sleep comfort mode on/off (air conditioner)
  --dryer DRYER         dryer mode on/off (air conditioner)
  --eco-mode ECO_MODE   eco mode on/off (air conditioner)
  --fahrenheit FAHRENHEIT
                        use Fahrenheit degrees on/off (air conditioner)
  --horizontal-swing HORIZONTAL_SWING
                        fan left/right swing on/off (air conditioner)
  --purifier PURIFIER   dryer mode on/off (air conditioner)
  --show-screen SHOW_SCREEN
                        display on/off (air conditioner)
  --target-temperature TARGET_TEMPERATURE
                        A/C target temperature (air conditioner)
  --turbo TURBO         turbo (boost) mode on/off (air conditioner)
  --turbo-fan TURBO_FAN
                        turbo fan mode on/off (air conditioner)
  ```  
  
  - Lorsque vous voyez on/off, il faut mettre respectivement 1 ou 0.  
  - Pour le cas particulier du FAN_SPEED, il faut être entre 20 et 80 (certains modèles acceptent 100) et il faut utiliser **102** si vous voulez mettre la ventilation en automatique.  
  - La température de consigne TARGET_TEMPERATURE peut-être de type entier 20 ou plus précis comme 20.5 avec un point pour séparer les décimales (pas la virgule) et évitez les dixièmes de degrés, restez sur du demi degré.  
  - Le mode est un chiffre à mettre, pour les clims c'est:  
    - auto = 1  
    - cool = 2  
    - dry = 3  
    - heat = 4  
    - fan_only = 5  

  - Pour les déshumidificateurs c'est:  
    - target = 1  
    - continu = 2  
    - smart = 3  
    - dryer = 4  

A vous de faire attention avec les possiblités, fiez-vous à l'appli pour ne choisir que des commandes acceptées par votre appareil.  

Voici un second exemple de code à mettre dans un scénario sans déclencheur, qui sera appelé par "Action de chauffe" dans le plugin Thermostat.  

![image](https://user-images.githubusercontent.com/3704897/205890404-5a87ac42-26e2-4cfc-ac69-5b786416a9c4.png)  
  
Réalisé par JulienB80, utilisateur et collaborateur au développement du plugin:  

<details markdown='1'>
<summary>Cliquez pour voir le code pour le scénario hiver</summary>

```php
// Par JulienB80 - 12/2022
// Les sondes midea étant peu fiables, tout se base sur un thermostat annexe géré par le plugin thermostat
// De plus, cela évite les commandes à répétition car tout est envoyé d'un coup.
// Pas de problème de cloud de cette manière.

// #########################################################################################
// ne changez que les éléments dans cet encart
  
//récupération de la puissance du thermostat
$cmdPower = cmd::byString("#[ChauffageClimatisation][Thermostat toto][Puissance]#");
$statePower = $cmdPower->execCmd();

//récupération de la consigne demandée à ce thermostat
$cmdConsigne = cmd::byString("#[ChauffageClimatisation][Thermostat toto][Consigne]#");
$stateConsigne = $cmdConsigne->execCmd();

// La commande citée plus haut pour envoyer les commandes personnalisées à votre appareil midea
$cmdPac = cmd::byString("#[ChauffageClimatisation][PAC toto][Commandes personnalisées]#");

// #########################################################################################

$scenario->setLog("Début d'exécution Bloc Code : Consigne : ".$stateConsigne."°C // Puissance :".$statePower."%");

// Si thermostat coupé, on coupe aussi la PAC
if ($statePower == 0) {
    $cmdPac->execute(array('text'=> '--running 0'));
    $scenario->setLog("Puissance Demandée : ".$statePower." % donc extinction PAC");
}

// Si peu de puissance demandée,
// on met une vitesse de ventilation faible
// petite correction sur température demandée
if (($statePower > 0) AND ($statePower <= 25))  {
    $temperature = $stateConsigne + 3;
    if ($temperature > 30)  {
          $temperature = 30;
    }
    $cmdPac->execute(array('text'=> '--mode 4 --turbo 0 --running 1 --fan-speed 40 --target-temperature '.$temperature));
    $scenario->setLog("Puissance Demandée : ".$statePower." % donc fan-speed = 40 + target-temperature ".$temperature.'°C');
}

// Si un peu plus de puissance demandée,
// on met une vitesse de ventilation normale
// moyenne correction sur température demandée
if (($statePower > 25) AND ($statePower <= 50))  {
    $temperature = $stateConsigne + 4;
    if ($temperature > 30)  {
          $temperature = 30;
    }
    $cmdPac->execute(array('text'=> '--mode 4 --turbo 0 --running 1 --fan-speed 60 --target-temperature '.$temperature));
    $scenario->setLog("Puissance Demandée : ".$statePower." % donc fan-speed = 60 + target-temperature ".$temperature.'°C');
}

// Si puissance demandée assez importante,
// on met une vitesse de ventilation forte
// moyenne correction sur température demandée
if (($statePower > 50) AND ($statePower <= 75))  {
    $temperature = $stateConsigne + 5;
    if ($temperature > 30)  {
          $temperature = 30;
    }
    $cmdPac->execute(array('text'=> '--mode 4 --turbo 0 --running 1 --fan-speed 80 --target-temperature '.$temperature));
    $scenario->setLog("Puissance Demandée : ".$statePower." % donc fan-speed = 80 + target-temperature ".$temperature.'°C');
}

// Si puissance demandée très importante,
// on met le mode turbo
// forte correction sur température demandée
if ($statePower > 75) {
    $temperature = $stateConsigne + 6;
    if ($temperature > 30)  {
          $temperature = 30;
    }
    $cmdPac->execute(array('text'=> '--mode 4 --turbo 1 --running 1 --fan-speed 80 --target-temperature '.$temperature));
    $scenario->setLog("Puissance Demandée : ".$statePower." % donc fan-speed = 80 + target-temperature ".$temperature.'°C + Turbo');
}
```
</details>
  
# Scripts Tiers  
  
Mideawifi repose sur le script tiers npm **midea-beautiful-air** en version *v0.9.15*  
Vous pouvez trouver le code github original ici:  [nbogojevic/midea-beautiful-air](https://github.com/nbogojevic/midea-beautiful-air)  
  
# Informations complémentaires  
  
 - Le plugin n'a pas été testé avec tous les climatiseurs et avec toutes les configurations logicielles et réseaux.  
 Merci de faire un Issue sur [GitHub](https://github.com/ddelec24/mideawifi/issues) ou un message sur le forum [Community Jeedom](https://community.jeedom.com/tag/plugin-mideawifi) si jamais vous constatez un dysfonctionnement.  
  
## Aide - FAQ  
  
### La température est incorrecte  
Dans votre application aussi. Sur beaucoup de modèles les capteurs sont mal placés dans les unités.  
  
### Il y a un délai entre les actions sur jeedom et l'effet sur l'appareil  
Effectivement, la détection peut mettre jusqu'à 20-30secondes, la récupération d'informations et les envois entre 5 et 15secondes. Tout dépend de la rapidité de réponse du cloud.  
  
### Depuis un redémarrage de jeedom ou de mon routeur, ça ne fonctionne plus.  
Il est fortement conseillé de fixer les adresses ip de vos équipements. C'est la première chose à vérifier.
  
## Problèmes connus

- Le cloud midea n'est pas connu pour être très robuste. Si vous faites 5 commandes en moins d'une minute, il risque de ne pas apprécier et n'en faire que la moitié!  
- Actuellement il faut mettre les identifiants midea air / nethome plus. Il semblerait que Msmarthome ne soit pas totalement compatible.  

---------------------------------------------------------------
Pour toutes autres questions, merci de regarder si il n'y a pas déjà une réponse à votre interrogation, sinon demandez sur le [community jeedom](https://community.jeedom.com)
