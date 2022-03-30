# Reduire la taille des paquets du jeu

Quelle que soit la plate-forme visée par votre projet UE4, la réduction de la taille du jeu emballé peut être un défi. Dans le guide suivant, nous allons couvrir les étapes que vous pouvez prendre pour aider à réduire la taille du paquet final de vos projets pour être aussi petit que possible en utilisant rien d'autre que les outils fournis à vous dans l'éditeur UE4.

## Créer un nouveau projet vierge
Lorsque vous commencez à travailler sur votre projet, vous pouvez être tenté d'utiliser un projet existant comme base de travail ou de créer un nouveau projet avec le contenu de démarrage activé. Ne faites pas cela, créez plutôt un projet entièrement nouveau, vide, basé sur C++ ou Blueprint, puis utilisez l'outil de migration pour transférer le contenu que vous souhaitez utiliser. De cette façon, vous vous assurez que le seul contenu de votre projet est celui qui doit s'y trouver. 

## Compression du contenu "cooked"

Le moyen le plus simple et le plus rapide de réduire la taille de vos paquets APK est de dire à UE4 de compresser les paquets APK pendant le processus d'emballage. Pour activer la compression des paquets, vous devez effectuer les opérations suivantes dans l'éditeur UE4. 

1. Tout d'abord, ouvrez les paramètres du projet en allant dans la barre d'outils principale et en sélectionnant l'option Editer, puis les paramètres du projet.   
2. Sous la section Projet, cliquez sur la section **Packaging** pour afficher les options de conditionnement du projet.   
3. Cliquez sur les **Advanced Properties** qui se trouvent en bas des paramètres de **Packaging** pour exposer les paramètres avancés du projet. 
4. Recherchez l'option intitulée **Create compressed cooked packages** et activez-la (si elle n'est pas déjà activée). 

Si vous n'avez pas packagé votre jeu avec la case **Create compressed cooked packages** activée, vous devriez voir une énorme différence de taille lorsque votre projet est empaqueté à nouveau avec cette option activée. En fait, il n'est pas rare que la taille des paquets APK de certains projets soit réduite jusqu'à 50 % lorsque la case **Create compressed cooked packages** est activée. 

## Shaders et bibliothèques de matériaux partagés
L'activation des options *Share Material Shader Code* et *Share Material Native Libraries* permet de réduire la taille globale du package de votre projet, mais au prix d'une augmentation des temps de chargement. Pour activer cette option dans votre projet UE4, vous devez procéder comme suit :

![[Packing_Share_Material_Code.jpg]]

## Exclusion du contenu de l'éditeur
En activant cette option, vous vous assurez qu'aucun des contenus utilisés par l'éditeur UE4 ne sera intégré à votre projet. Notez que l'activation de cette option pourrait causer des problèmes de contenu manquant dans les projets qui pourraient utiliser le contenu de l'éditeur. Pour activer ces deux options dans votre projet UE4, vous devez procéder comme suit : 

![[Packing_Exclude_Editor_Content.jpg]]

## Configurer les niveaux d'un projet
Un aspect souvent négligé qui peut mener à l'augmentation de la taille des paquets APK de vos projets est le fait de ne pas configurer correctement les options du projet, comme le niveau qui doit être utilisé par défaut, ou le niveau utilisé pour les transitions de niveau. Pour définir le niveau (ou les niveaux) à utiliser pour ce type d'interaction, vous pouvez procéder comme suit. 

+ Sous Projet, dans la section Maps & Modes, recherchez la section **Default Maps**.

![[T_Set_Maps.png]]

## Sélection du contenu à packager
Dans la section "Packaging" des paramètres de votre projet, vous pouvez indiquer quelles cartes et quels contenus doivent ou non être inclus dans votre jeu. Pour spécifier les cartes qui doivent être incluses dans votre projet, vous devez procéder comme suit : 

+ Faites défiler la partie inférieure des options avancées d'empaquetage jusqu'à ce que vous voyiez une case cochée pour l'option ***List of maps to include in a packaged build***. Les options que vous voyez ici vous permettront de spécifier le contenu et les cartes qui doivent être emballés ou non avec votre projet. 

![[Selected_Item_Location.png]]
