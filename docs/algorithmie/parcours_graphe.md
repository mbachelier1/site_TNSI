# Algorithmes de parcours de Graphes
## Parcours en largeur d'abord (Breadth First Search - BFS)
Le principe du parcoursen largeur d'abord est de choisir un sommet et de parcourir les noeuds en listant les noeuds de même profondeur par rapport au noeud de départ.
![anim BFS](img/bfs.gif)

A partir de A on explorera d'abord les voisins directs (B et C) puis les voisins de profondeur 2 par rapport à A, soit D et E, puis les noeuds de profondeur 3 soit F et G et enfin H. 

!!! caution "Etapes de la procédure"
	On crée une file vide

	1. On enfile le nœud de départ.  
	2. On enfile les nœuds adjacents s'ils ne sont pas déjà présents dans la file et qu'ils n'ont pas déjà été visités (on créera une liste pour y stocker les noeuds visités)  
	3. On défile (c'est-à-dire on supprime la tête de file).  
	4. Tant que la file n'est pas vide, on ré-itère les points 2 et 3.  
	5. On affiche la liste des noeuds visités  


!!! faq "à partir d'autres noeuds"
	Développer l'algorithme en partant des noeuds H puis D.

L'algorithme en pseudocode :
```pseudocode
VARIABLE
G : un graphe
s : noeud (origine)
u : noeud
v : noeud
f : file (initialement vide)

//On part du principe que pour tout sommet u du graphe G, u.couleur = blanc à l'origine
DEBUT
s.couleur ← noir
enfiler (s,f)
tant que f non vide :
    u ← defiler(f)
    pour chaque sommet v adjacent au sommet u :
        si v.couleur n'est pas noir :
            v.couleur ← noir
            enfiler(v,f)
        fin si
    fin pour
fin tant que
FIN
```

## Parcours en profondeur d'abord (Deep First Search - DFS)
Pour ce parcours, on explore les voisins du noeuds de départ un par un et on explore les voisins du premier voisin, puis ceux du deuxième, ...
![anim DFS](img/dfs.gif)
On démarre du noeud a, on explore b jusqu'au bout soit e puis f puis g puis h. En arrivant sur une feuille on remonte au deuxieme voisin de a, c qui n'a pas d'autres voisins non déjà visités.


!!! caution "Etapes de la procédure"

	1. On part d'un sommet que l'on empile;  
	2. On dépile et on marque le sommet dépilé comme traité (il faudrait créer une liste pour les sommets déjà traités)  
	3. On empile chacun des voisins du sommet dépilé qui ne sont pas déjà dans la pile et qui n'ont pas été déjà été traités;  
	4. On recommence à partir du point 2 tant que la pile n'est pas vide.  

!!! faq "à partir d'autres noeuds"
	Développer l'algorithme en partant des noeuds H puis D.


L'algorithme itéraif en pseudocode
```pseudocode
VARIABLE
s : noeud (origine)
G : un graphe
u : noeud
v : noeud
p : pile (pile vide au départ)
//On part du principe que pour tout sommet u du graphe G, u.couleur = blanc à l'origine
DEBUT
s.couleur ← noir
piler(s,p)
tant que p n'est pas vide :
u ← depiler(p)
pour chaque sommet v adjacent au sommet u :
    si v.couleur n'est pas noir :
        v.couleur ← noir
        piler(v,p)
    fin si
fin pour
fin tant que
FIN
```

L'algorithme récursif en pseudocode
```pseudocode
VARIABLE
G : un graphe
u : noeud
v : noeud
//On part du principe que pour tout sommet u du graphe G, u.couleur = blanc à l'origine
DEBUT
PARCOURS-PROFONDEUR(G,u) :
  u.couleur ← noir
  pour chaque sommet v adjacent au sommet u :
    si v.couleur n'est pas noir :
      PARCOURS-PROFONDEUR(G,v)
    fin si
  fin pour
FIN
```

## Chercher son chemin
Chercher son chemin dans un graphe c'est parcourir le graphe en mémorisant les noeuds par lesquels on passe, en s'arrêtant dès que l'on a rencontré le noeud d'arrivée.

!!! hint "algorithme"
	```pseudocode
	Fonction cherche_chemin(graphe,depart,arrivee)  
	    P ← pile vide  
	    empiler le couple (depart,[depart]) dans P  
	    chemin ← liste vide  
	    Tant que P n'est pas vide faire  
	        (sommet,chemin) ← on dépile P  
	        listes_nouveaux_sommets_voisins ← liste des sommets   adjacents à sommet qui ne sont pas dans chemin (liste réinitialisée à chaque tour)  
	        Pour un_sommet dans listes_nouveaux_sommets_voisins  
	            Si un_sommet = arrivee alors  
	                retourner chemin + [un_sommet]  
	            sinon  
	                empiler (un_sommet,chemin + [un_sommet])  
	            FinSi  
	        FinPour  
	    FinTantQue  
	FinFonction
	```

## Chercher tous les chemins
Le principe est le même que précédemment mais on ne s'arrête pas dès que le noeud est rencontré. On mémorise le chemin et on continue de parcourir le graphe de façon à rencontrer encore le noeud d'arrivée.
On place les chemins trouvés dans une liste et on retourne cette liste.


!!! hint "algorithme"
	```pseudocode
	Fonction cherche_chemin(graphe,depart,arrivee)  
	    P ← pile vide  
	    L ← liste vide
	    empiler le couple (depart,[depart]) dans P  
	    chemin ← liste vide  
	    Tant que P n'est pas vide faire  
	        (sommet,chemin) ← on dépile P  
	        listes_nouveaux_sommets_voisins ← liste des sommets   adjacents à sommet qui ne sont pas dans chemin (liste réinitialisée à chaque tour)  
	        Pour un_sommet dans listes_nouveaux_sommets_voisins  
	            Si un_sommet = arrivee alors  
	                ajouter chemin + [un_sommet]  à L
	            sinon  
	                empiler (un_sommet,chemin + [un_sommet])  
	            FinSi  
	        FinPour  
	    FinTantQue  
	    Retourner L
	FinFonction
	```

!!! note "Remarque"
	Le chemin le plus court sera celui contenant le moins de noeuds rencontrés.

## Détection de cycle
Un cycle dans un graphe est un chemin dont le neoud de départ et le noeud d'arrivée sont identique. le principe étant de ne JAMAIS faire demi tour donc de ne pas revenir sur des noeuds déjà visités.

Si on veut chercher tous les cycles à partir d'un sommet on applique l'algorithme de recherche de tous les chemins. Et si on veut tous les ycles du graphe, on appique ce dernier à tous les sommets.

!!! hint "algorithme"
	```pseudocode
	Fonction rechercher_cycle(graphe,sommet):
	    cycle<-liste vide
	    Pour tous les voisins de sommet
	        chercher tous les chemins entre sommet et voisin
	    FIN Pour
	    Pour chaque chemin trouvé :
	        ajouter à cycle (chemin+sommet)  
	    FIN POUR
	    Revoyer cycle
	FIN FONCTION
	```