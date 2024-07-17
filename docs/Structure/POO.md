# Programmation Orientée Objet (POO)

*Tous les bouts de codes sont à tester dans un progrmme python pour se rendre compte du résultat*

La programmation orientée objet est une méthode de programmation qui consiste à créer des objets qui auront des caractéristiques et des méthodes bien spécifiques à ce type d'objet. Par exemple, les chaîne de caractères en python sont des objets. On peut en créer une, la supprimer, accéder à sa longueur, ajouter des éléments, compter des occurences, ... Le type str en python est en réalité un objet avec ses propres caractéristiques et méthodes.  

Nous allons prendre un exemple et le développer pas à pas.  

Dans cet exemple, nous allons utilisé la gestion d'un parc automobile. Chaque voiture du parc aura les caractéristiques suivantes : **marque, modèle, couleur, année, propriétaire, prix neuf**. On pourra modifier ces caractéristiques en **vendant** ou **repeignant** et **déterminer sa côte** en fonction de l'année.  


## Création de la classe
La classe est le moule qui va nous permettre de abriquer des objets ayant accès aux mêmes caractéristiques et méthodes.
```python
class Voiture:
    marque="Peugeot"
#on créé un moule appelé voiture dont l'attribut marque vaut "Peugeot"
#On crée des voitures à partir ce moule
voiture_de_papa=Voiture()
voiture_de_maman=Voiture()
voiture_de_papa.marque #affiche la marque renseignée lors de la création de la voiture (ici par défault Peugeot).
```
On peut modifier la valeur de l'attribut :
```python
voiture_de_maman.marque="citroen"
```

!!! success "Vocabulaire"
	`voiture_de_maman` et `voiture_de_papa` sont des instances de la classe `Voiture`. Ce sont des obets fabriqués à partir du moule `Voiture`.

## Méthode et `self`
Une méthode prend toujours en premier paramètre l'objet lui-même par l'intermédiare de l'argument `self`.
L'appel de la méthode se fait également avec la notation : `nom_instance.methode(...)`

```python
class Voiture:
    marque="Peugeot"
    def ajoute_modele(self,modele):
        self.marque=self.marque+ ' ' + modele
        return self.marque
voiture_de_maman=Voiture()
voiture_de_maman.ajoute_modele("c4")
voiture_de_maman.marque
```

## Constructeur


Le constructeur `__init__` permet de créer des objets dont les attributs seront différents. On va prendre un exemple :
```python
class Personne:
    def __init__(self, nom, age):
        self.nom = nom
        self.age = age

jim = Personne("Jim", 27)

print(jim.nom)
print(jim.age) 
```

!!! note "Remarque"
	Pour afficher la totalité des attributs de la classe en une seule fois, on serai tenté de faire `print(jim)`. Mais le résultat n'est as concluant.

La méthode `print()` appelle une méthode de classe appelée `__repr__`. On va modifier cette méthode pour que tout l'objet s'affiche. 
```python
class Personne:
    def __init__(self, nom, age):
        self.nom = nom
        self.age = age
    def __repr__(self):
        return f"{self.nom} est une Personne de {self.age} ans."

john = Personne("John", 32)

print(john)
```

## Méthodes spécifiques à l'objet


On peut créer des méthodes dans la classes permettant par exemple de modifier certains attributs.  
Etudier le code suivant :
```python


class Personne:
    def __init__(self, nom, annee):
        self.nom = nom
        self.annee = annee
        self.age=None
    def calculer_age(self,annee_courante):
        self.age=annee_courante-self.annee
        return f"{self.nom} a {self.age} ans"
    def renommer(self,nouveau_nom):
        self.nom=nouveau_nom
    def __repr__(self):
        return f"{self.nom} est une Personne né en {self.annee}."

pierre = Personne("pierre", 1985)
print(pierre)
pierre.renommer("paul")
print(pierre.nom)
print(pierre.calculer_age(2021))
print(pierre.age)

```
La méthode `renommer()` permet de modifier la valeur de l'attribut `nom` de l'instance créée. La méthode `calculer_age` permet de mettre l'âge à jour. 

!!! note "année courante"
	On pourrait même faire appel au module `datetime` pour accéder à l'année courante et mettre à jour l'âge automatiquement.
	```python
	import datetime
	date=datetime.datetime.now()
	annee_courante=date.year
	print(pierre.calculer_age(annee_courante))
	```

## Getteurs et setters : les bonnes pratiques
En réalité, si l'on souhaite modifier les attributs :  
`get_nom_attribut`: pour le récupérer.  
`set_nom_attribut`: pour le modifier.  
```python
class Personne:
    def __init__(self, nom, age):
        self.nom = nom
        self.age = age
    
    def get_nom(self):
        return self.nom
    
    def set_nom(self, nom):
        self.nom = nom
    
    def get_age(self):
        return self.age
    
    def set_age(self, age):
        self.age = age
        
    def __repr__(self):
        return f"{self.nom} est une Personne de {self.age} ans."

john = Personne("John", 32)

print("Au début")
print(john)

print("Modification des attributs avec les setters")
john.set_nom("Jean")
john.set_age(12)
print(john)

print("Récupération des attributs avec les getters")
john.get_nom(), john.get_age()
```

## A retenir

![moule](img/moule.png){align=left}

La POO permet la fabrication d'objets issus d'un même moule mais personnalisable en modifiant certaines caractéristiques et d'adapter le programme à chaque situation.
Tout python est en fait encapsulé dans des objets.

### vocabulaire
**La classe** : c'est le moule à partir du quel on fabrique les objets.  
L'**objet est une instance de la classe**, un même moule peut fabriquer plusieurs objets.  
Les **attributs** : caractéristiques personnalisables des objets.  
Les **méthodes**  sont des actions que l'on peut réaliser sur les objets.  

### Créer une classe
**Sans consructeur**
```python
class Sandwich:
	sauce="blanche"
	pain="pita"
	legume="tomate"
	viande"steack haché"

```
Tous les objets créés auront les mêmes attributs que l'on pourra modifier ensuite.
On peut remplacer les valeurs par défaut par None.

**Avec constructeur**
```python
class Sandwich:
	def __init__(self,sauce,viande,pain,legume):
		self.sauce=sauce
		self.pain=pain
		self.viande=viande
		self.legume=legume
```
On donne aux objets des attributs précis dès la création
A chaque utilisation de la méthode self est remplacé par le nom de l'instance.

### créer une instance de classe
Chaque sandwich créé est une instance de la classe `sandwich`.
```python
vegie=Sandwich("blanche","staeck de soja","pita","salade")
```

!!! note "Remarque"
	Sans constructeur, on ne mettra pas d'arguments mais les valeurs des attributs seront celles définies par défaut.

!!! warning "Instance de classe"
	`Vegie` est une instance de la classe sandwich.

### Créer et appeler uen méthode
```python
class Sandwich:
	def __init__(self,sauce,viande,pain,legume):
		self.sauce=sauce
		self.pain=pain
		self.viande=viande
		self.legume=legume
	def afficher(self):
		L=[]
		L.append(self.sauce)
		L.append(self.pain)
		L.append(self.viande)
		L.append(self.legume)
		return L
vegie=Sandwich("blanche","staeck de soja","pita","salade")
#on appelle la méthode
print(vegie.afficher())
```
Cet appel affiche :  
['blanche', 'pita', 'steack de soja', 'salade']

### Getteurs et setters
C'est la manière la plus "propre" d'accéder et de modifier les attributs d'instance.  

```python
class Sandwich:
	def __init__(self,sauce,viande,pain,legume):
		self.sauce=sauce
		self.pain=pain
		self.viande=viande
		self.legume=legume
	def get_pain(self):
		return self.get_pain
	def set_pain(self,pain):
		#remplace la valeur précédente de l'attribut pain par celui passé en argument
		self.pain=pain
	def afficher(self):
		L=[]
		L.append(self.sauce)
		L.append(self.pain)
		L.append(self.viande)
		L.append(self.legume)
		return L
vegie=Sandwich("blanche","staeck de soja","pita","salade")
print(vegie.get_pain())
vegie.set_pain("galette")
print(vegie.get_pain())
```
Le premier appel affiche 'pita' le second 'galette'.

!!! tip "récapitulatif de la syntaxe"
	```python
	class MaClasse:  
		attribut=…
	```
	Créer une instance de classe : 
	```python
	instance=MaClasse(args)
	```
	Créer une méthode :
	```python
	def methode(self,args):
	return …
	```
	Appeler une méthode sur une instance : 
	```python
	objet.methode()
	```
	Accéder à un attribut d'une instance :
	```python
	instance.attribut
	```
	Constructeur :
	```python
	def __init__(self,arg1,arg2):
		self.attribut1=arg1
		self.attribut2=arg2
	```
	Accéder à un attribut d'instance (getters)
	```python
	def get_attribut(self):
		return self.attribut
	instance.get_attribut()
	```
	Modifier un attribut d'instance
	```python
	def set_attribut(self,arg):
		self.attribut=arg
	instance.set_attribut(arg)
	```
