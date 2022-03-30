# Reduire la taille des paquets du jeu

Quelle que soit la plate-forme visée par votre projet UE4, la réduction de la taille du jeu emballé peut être un défi. Dans le guide suivant, nous allons couvrir les étapes que vous pouvez prendre pour aider à réduire la taille du paquet final de vos projets pour être aussi petit que possible en utilisant rien d'autre que les outils fournis à vous dans l'éditeur UE4.

## Créer un nouveau projet vierge
Lorsque vous commencez à travailler sur votre projet de mobile Android, vous pouvez être tenté d'utiliser un projet existant comme base de travail ou de créer un nouveau projet avec le contenu de démarrage activé. Ne faites pas cela, créez plutôt un projet entièrement nouveau, vide, basé sur C++ ou Blueprint, puis utilisez l'outil de migration pour transférer le contenu que vous souhaitez utiliser. De cette façon, vous vous assurez que le seul contenu de votre projet est celui qui doit s'y trouver. 

## Compression du contenu "cooked"

Le moyen le plus simple et le plus rapide de réduire la taille de vos paquets APK est de dire à UE4 de compresser les paquets APK pendant le processus d'emballage. Pour activer la compression des paquets, vous devez effectuer les opérations suivantes dans l'éditeur UE4. 

1. Tout d'abord, ouvrez les paramètres du projet en allant dans la barre d'outils principale et en sélectionnant l'option Editer, puis les paramètres du projet.   
2. Sous la section Projet, cliquez sur la section **Packaging** pour afficher les options de conditionnement du projet.   
3. Cliquez sur les **Advanced Properties** qui se trouvent en bas des paramètres de **Packaging** pour exposer les paramètres avancés du projet. 
4. Recherchez l'option intitulée **Create compressed cooked packages** et activez-la (si elle n'est pas déjà activée). 

Si vous n'avez pas packagé votre jeu avec la case **Create compressed cooked packages** activée, vous devriez voir une énorme différence de taille lorsque votre projet est empaqueté à nouveau avec cette option activée. En fait, il n'est pas rare que la taille des paquets APK de certains projets soit réduite jusqu'à 50 % lorsque la case **Create compressed cooked packages** est activée. 