
# CHANGELOG BETA

## 06/10/2023 - Fix: Problème de compatibilité entre plusieurs librairies python3.  
Permet de résoudre l'erreur `cannot import name 'url_quote' from 'werkzeug.urls'`.  
Si vous avez ce soucis, relancez les dépendances et le service, sinon ne touchez à rien.  

## 10/01/2023 - Work in Progress - Tentative d'implémentation MsmartHome  
- Les équipements qui sont appairés avec l'application MsmartHome n'arrivent pas à communiquer correctement.  
Première beta sur cette fonctionnalité: Possibilité de cocher MsmartHome dans la configuration générale du plugin.  
Seul le discover est accessible avec cette fonctionnalité. Merci de me faire un retour des logs en debug si vous êtes dans l'obligation d'utiliser cette application.  
  
## 09/01/2023 - Possibilités de cron  
- Depuis la page de configuration, on a maintenant le choix entre 3 cron, 1 minute, 5 minutes ou 10 minutes pour la récupération des informations.  
Fonctionnalité en test, à voir si les testeurs qui mettent 1 minute ont des soucis de remontés d'informations ou non.  
  
## 03/12/2022 - Ajout Déshumidificateur  
- Ajout des fonctions de base pour déshumidificateur (merci Ludi)  
- Ajout de la possibilité d'activer ou désactiver l'affichage sur les clims (non visible par défaut - demande de Fifi.h)  
- switch entre °C et °F caché par défaut

## 30/11/2022 - Mise en beta de la refonte du plugin 
- /!\ Rappel: si vous avez déjà le plugin mideawifi en beta avant cette date, il faut supprimer les équipements, faire la mise à jour et suivre la documentation comme un nouveau plugin!  
- Fonctionnement satisfaisant pour une utilisation avec les clims. Les déshumidificateurs arriveront dans la fin de semaine.
- Mise à jour documentation en conséquence.  

## 06/11/2022 - REFONTE PLUGIN  
  
+ Utilisation d'un package npm _midea-beautiful-air_ que j'ai dockerisé pour avoir une communication plus simple et surtout une compatibilité avec jeedom (car le script nécessite python3.8 minimum)  
+ Compatibilité arm / raspberry OK
+ récupération et création des équipements OK
+ WIP: enregistrement des commandes infos + actions, dashboard.
