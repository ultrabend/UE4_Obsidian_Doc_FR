# Widget Blue Print

	Notion Importante à prendre en compte pour l'initialisation du widget

Certaines Blueprints sont invoqué à l'initialisation mais ont des niveaux differents.

**Event Construct**
Appelé après la construction du widget. Selon la façon dont l'objet est utilisé, cet événement peut être appelé plusieurs fois en raison de l'ajout et de la suppression de la hiérarchie. Si vous avez besoin d'un véritable événement appelé une seule fois lors de la création, utilisez OnInitialized.

**OnInitialized**
Appelé une seule fois au moment du jeu sur les instances qui ne sont pas des modèles. Alors que Construire/Détruire concerne les parties sous-jacentes, ceci n'est appelé qu'une seule fois pour l'UUserWidget. Si vous avez des choses uniques à établir à l'avance (comme lier des callbacks aux événements sur les propriétés du BindWidget), faites-le ici.