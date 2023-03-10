# Changelog plugin Signal  
  
    
> **IMPORTANT**  
>    
> S'il n'y a pas d'information sur la mise à jour, c'est que celle-ci concerne uniquement de la mise à jour de documentation, de traduction ou de texte.  

# 10/03/2023  
  - Fix: Problème de redémarrage du container docker après une mise à jour ou un redémarrage de jeedom.  
  - Ajout: On peut désormais fournir un flux RTSP qui va durer 10sec avant d'être envoyé (voir documentation pour l'usage).  
  
# 27/01/2023  
  - Amélioration: Les groupes n'ayant pas de nom ne sont plus synchronisés.  
  
# 22/01/2023  
  - Nouvelle fonctionnalité: Cron journalier pour récupérer le dernier message. Lorsque l'on est pas en réception automatique des messages, il faut quand même recevoir un message régulièrement pour que la liaison fonctionne (désactivation si pas de réception dans les 35 derniers jours). Permet aussi la synchronisation des groupes sans avoir activé la réception automatique des messages. 
  
# 19/01/2023  
  - Amélioration: évite une erreur dans le fichier de log **http.error** lorsqu'on reçoit un message trop long. Message tronqué à 115 caractères maintenant.  
  - Fix: Lors de la suppression d'un numéro, on supprime les fichiers laissés par le service API en même temps.  
 
# 18/01/2023  
  - FIX: Dans certaines situations, des guillemets ou caractères spéciaux (retour ligne) pouvaient générer des erreurs dans jeedom.  
  
# 14/01/2023  
  - Possibilité d'envoi de fichiers depuis des commandes d'autres plugins (camera par exemple)  

# 29/12/2022  
  - Support des groupes. Il est désormais possible d'envoyer un message à un groupe signal. Voir documentation pour la mise en place.  

# 16/12/2022  
  - FIX: Suite redémarrage de la machine, le service ne se relançait pas seul. à Vérifier si la correction est fonctionnelle pour tous. (Il faut relancer les dépendances)  

# 14/12/2022  
  - Les retours à la ligne dans les messages sont désormais bien pris en comptes  
  
# 22/11/2022  
  - Upgrade du signal REST API en version 0.64  

# VERSION INITIALE - 16/09/2022
