# Le Pipeline
Le rendu temps réel est une méthode de représentation pour laquelle chaque image est rendue dans les millisecondes qui précédent son affichage. Chaque image (ou _Frame_) est le résultat d’un travail effectué à la fois par le CPU et le GPU.

Et concrètement pour Unreal ? Et bien le _Pipeline_ est composé de plusieurs étapes qui se transmettent des informations afin de peindre un joli rendu 2D de votre monde 3D.

Le schéma ci-dessous résume la forme de ce _Pipeline_.

![[Pipeline-1024x576.jpg]]

Le rôle du _pipeline_ est de générer des images. Chaque image rendue est le résultat d’un travail effectué à la fois par le CPU et le GPU. Pour simplifier, le CPU prépare les données et émet des _DrawCalls_ que le GPU doit traiter. Un _DrawCall_ est une requête pour dessiner des maillages donnés à l’écran (ou dans une mémoire tampon), en utilisant des _Shaders_ spécifiques. Pour le traitement de ces _Shaders_, Unreal ne peut pas contrôler directement le GPU, il doit plutôt envoyer des commandes à celui-ci. Dans le cas des PC et des mobiles, ces appels de fonctions sont traduites par un pilote graphique. En ce qui concerne les données, la mémoire du GPU est une pièce de matériel physiquement séparée, c’est la RAM vidéo, aussi appelée VRAM. Il est donc nécessaire de déplacer les données entre la RAM du système principal et la VRAM.

Tout cela signifie que l’unité graphique doit attendre la fin du travail du CPU. Mais attention ! Elle ne peut commencer à dessiner qu’après :

- Que le code de rendu du moteur de jeu soit terminé (sur le CPU).
- Que les _DrawCalls_ soient traduits en code GPU
- Et que les données nécessaires soient transférées de la RAM à la VRAM (si elles n’y étaient pas déjà présentes)

Lorsque tout ceci sera prêt, la carte graphique pourra commencer à faire son travail.

![[before_rendering.jpg]]

Une fois le travail des _Shaders_ terminé on passe à la Pixellisation (_Rasterization_). Le principe est le suivant, la zone appartenant à un triangle donné dans l’espace de l’écran est remplie pixel par pixel. La couleur résultante est une sortie directe du programme de _Shaders_. Il n’a aucune connaissance des autres triangles de la scène. Il ne peut travailler qu’avec les données venant du _Vertex Shader_ et des textures, qui lui sont fournies en entrée.

## Pipeline : **Shader Deferred ou Forward ?**
Il existe 2 méthodes pour effectuer un rendu, il y a le _Forward Rendering_ (Directe) et le _Deferred Rendering_ (Différée).

Le **Deferred shading** est la méthode par défaut de rendu des lumières et des matériaux dans Unreal. Par différé on entend que le traitement est réalisé dans une passe séparée, au lieu d’être réalisée dans les _Shaders_ de chaque objet. Ce type d’éclairage attend la passe de base pour accumuler les informations sur les objets opaques et leurs matériaux dans un G-Buffer. Il résout ensuite l’éclairage dans l’espace de l’écran, en une seule passe. Cette approche réduit le problème de performance lié à la superposition de plusieurs sources lumineuses qui est un problème typique du rendu direct. Leur impact est plus facile à prévoir et ne dépend pas du nombre d’objets dans la scène. Le coût d’une seule lumière dépend directement de la surface couverte par la lumière dans l’espace de l’écran. Cette technique est utilisée de façon grandissante dans les jeux vidéo en raison du contrôle qu’elle offre lorsqu’il s’agit d’utiliser un grand nombre de sources lumineuses.

Le **Forward Rendering** est l’ancienne méthode de rendu des moteur 3D temps réel et a été exploitée par la quasi-totalité des moteurs de jeux. C’est avec l’évolution des technologies, associée à la demande croissante de qualité graphique des productions, que les développeurs ont remis en question cette approche. Jusqu’à la version 3, l’Unreal Engine utilisait la méthode Forward.  
Avec cette méthode, tout le travail sur l’éclairage dynamique se fait dans la passe de base, au lieu d’une passe distincte pour les lumières. L’éclairage n’est plus reporté à plus tard, il est effectué immédiatement sur un niveau du _Shader_ de chaque objet, juste après le calcul des attributs du matériel final. Cette approche permet de se débarrasser du G-Buffer, d’économiser la mémoire du GPU et de faciliter plusieurs choses (notamment l’anticrénelage). En revanche, le coût de la passe de base est nettement plus élevé.

Voici un tableau non exhaustif des différences entre les 2 modes :

|                          **Deffered**                          |                                  **Forward**                                  |
|:--------------------------------------------------------------:|:-----------------------------------------------------------------------------:|
|         Il fonctionne dans la majorité des situations          | Donne de meilleurs performance pour des choses simples sur du hardware limité |
| Est plus stable et performant pour des applications gourmandes |                 L’anti aliasing MSAA est meilleurs en forward                 |
|                 Supporte énormément de shaders                 |                       Bonne gestion de la transparence                        |
|                    Est bien plus documenté                     |                                                                               |
|              Mauvaise gestion de la transparence               |                                                                               |

### Attention
Dans Unreal, le mode Deferred est le mode par défaut pour les applications PC.  
Cependant si l’emploi du mode Forward devient une nécessité, il peut être activé via les _Project Settings._

![[01-Deffered.jpg]]

