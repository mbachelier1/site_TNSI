# Calculabilité et décidabilité
## Programme en tant que donnée

Nous avons l’habitude d’utiliser les données et le programmes en les rangeant respectivement dans des variableset des fonctions.  
Par exemple :  
```python
def somme(a,b):
	c=a+b
	return c
```
`a, b et c` sont des données rangées dans des variables et `somme()` est une fonction dans laquelle on range quelques lignes de programme.

Or si on utlise la fonction `eval() ` qui prend en argument une chaîne de carctères : 
```python
>>> eval("8 + 2")
10

>>> eval('somme(3,3)')
6
```
Cette fonction permet de transformer  une chaine de caractères en programme et de l’éxecuter s’il est exécutable.  
Le programme que l’on a créé est donc rangé comme une donnée dans une variable de type `string`.   

**LE PROGRAMME EST DONC AUSSI UNE DONNEE**  

!!! question "Question"
	1.Trouver une ou des situations où le programme est considéré comme  une donnée.

## Calculabilité
Un problème est considéré comme calculable si on peut le coder dans un langage de programmation usuel.  
Certaines choses ne se calculent pas avec un ordinateur. Par exemple on ne peut pas calculer si une fonction va s'arréter, ni si un programme va provoquer une erreur.  

!!! question "Question"
	2.Chercher outre le probleme de l'arrêt un problème célèbre non calculable. 


## Décidabilité
Un problème de décision est dit décidable s'il existe un algorithme, une procédure mécanique qui se termine en un nombre fini d'étapes, qui le décide, c'est-à-dire qui réponde par oui ou par non à la question posée par le problème. S'il n'existe pas de tels algorithmes, le problème est dit **indécidable**.  
![decidabilité](img/decidabilite.png)  


!!! example "Par exemple"
	- un entier est-il pair ou non: ce problème est décidable car la réponse est oui ou non
	- un nombre est un nombre premier ou non


!!! warning "Attention"
	Un problème peut être théoriquement décidable sans l’être en pratique. parce que celle-ci nécessiterait trop de temps (plus que l'âge de l'univers) ou trop de ressources (plus que le nombre d'atomes de l'univers).


Donnons des exemples de problèmes non décidables. Je parcours un réseau aléatoirement, est-ce que je vais atteindre une cible données en un nombre fini d'étapes? Pas forcément, même si la probabilité d'arriver à destination tend vers 1 quand le nombre d'étapes tend vers l'infini!  

### Problème de l'arrêt

Un autre exemple plus connu: le problème de l'arrêt d'un programme est-il décidable? Est-ce que je peux écrire un programme qui me dira si un programme va s'arrêter ou non (selon les valeurs d'entrées)? Nous verrons que l'on peut prouver que ce problème n'est pas décidable: il n'existe pas d'algorihtme capable de prédire si n'importe quel programme va s'arrêter ou non. Cela vous plairez bien...n'avez vous jamais fait de boucle infinie?

<iframe width="560" height="315" src="https://www.youtube.com/embed/13O1qhX4Bqo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

!!! question "Question"
	3.Pourquoi le problème de l'arrêt est dit indécidable?  
	4.En quoi la phrase "je suis un menteur" illustre bien le problème du paradoxe?  

Etudiez le script suivant :

<iframe src="https://trinket.io/embed/python3/354bd83c3d" width="100%" height="356" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

!!! question "Question"
	5.Que se passe-t-il?


Supposons qu'il existe une fonction calculable `termine(fonction, données)` qui prend 2 arguments : une fonction, et des données d'entrée pour cette fonction 
et qui renverra `True` si le programme termine et `False` s'il entre dans une boucle infinie.  

On définit les deux fonctions suivantes :  
```python
def fonction1(n):
    if n % 3 != 0:
        return True
    else:
        return False

def fonction2(n):
    while n % 3 != 0:
        print("True")
    print("False")
```

!!! question "Question"
	6.Que renverront les appels suivants ?  
	`termine(function1, 7)`  
	 	`termine(function1, 9)`  
	 	`termine(function2, 7)`  
	 	`termine(function2, 9)`   
	Justifier vos réponses.

On définit une fonction `test_sur_soi`.  
```python
def test_sur_soi(programme):
    if termine(programme, programme):
        while True: pass # boucle infinie
```  

!!! question "Question"
	7.Que se passe-t-il si on appelle `test_sur_soi` sur elle-même: `test_sur_soi(test_sur_soi)` ?

!!! info "En complément pour ceux qui n'ont pas encore les neurones qui chauffent..."
	<iframe width="560" height="315" src="https://www.youtube.com/embed/Kf-IHn1PvaQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>