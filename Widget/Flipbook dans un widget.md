# FlipBook dans un widget

Integrer un Flipbook dans un Widget est en fait une démarche relativement simple.
Voici les différentes étapes :

## Création du Flipbook via une Material
Créer une nouvelle Material et définir ses propriétés en tant que ***User Interface***
ainsi que le Blend Mode en ***Translucent*** car la texture peut contenir de la transparence sur le canal Alpha


![[flipbook_mat_settings.png]]


Construire la Material avec les éléments suivants :

+ Une Texture Sample
+ Le bloc FlipBook auquel on indique les dimensions de la matrice de l'image flipbook


![[flipbook_mat.png]]

## Integration au Widget
Pour integrer le flipbook, il suffit d'inserer un ***Image*** et de selectionner notre Material Flipbook pour le paramètre Brush

![[flipbook_widget.png]]

Et le tour est joué !

![[flipbook_widget_brush.png]]