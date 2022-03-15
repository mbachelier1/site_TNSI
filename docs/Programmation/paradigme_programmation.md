# Paradigmes de programmation

Un paradigme de programmation est une méthode de programmation qui respecte certaines règles qu'il va falloir respecter.
On distinque parmi ces paradigmes :  
- la programmation [orientée objet](https://mbachelier1.github.io/site_TNSI/Structure/POO.html)  
- la programmation fonctionnelle  
- la programmation impérative  
- la [programmation évènementielle](https://mbachelier1.github.io/site_1NSI/IHM/javascript/programmation_evenementielle.html) : le programme exécuté va dépendre d'un évènement utilisateur (clic sur un bouton, prsser une touche du clavier, ...). Cela a été vu en 1ere lors que l'utilisation de `javascript`.  


## Pragrammation fonctionnelle vs programmation impérative
Le principe de la programmation fonctionnelle est de placer la totalité du code dans des fonctions. Certaines règles sont cependant à respecter :
- Une fonction ne doit pas modifier une variable, mais seulement les informations passées en argument  
- Les fonctions doivent être **pures** c'est-à-dire qu'un appel à une fonction avec le même argument doit **toujours** donner le même résultat. 
- Les fonctions peuvent appeler d'autres fonctions  
- On limite les variables globales et il n'y a pas de "programme principal" le programme doit s'exécuter uniquement par appel de fonctions  
- On ne fait pas de boucles, on utilise la récursivité à la place (nous n'irons peut etre pas aussi loin)  
En respectant ces règles on s'affranchit des effets de bord.    

!!! note "Effets de bords"
	Les effets de bords en informatique, sont en fait un effet non désirable ou non prévu par le programmeur. Ces effets arrivent souvent lorsque qu'une fonction manipule une variable globale.  

!!! example "Quelques exemples"
	Exemple 1 : modification d'une variable globale
	```python
	c=1
	def augmenter(n):
	    global c
	    c=c+n
	    return c
	print(augmenter(5))
	print(augmenter(5))
	```
	Les deux appels, pourtant identiques, de cette fonction ne revnoient pas la même valeur (le premier renvoie 6 et le second 11). Cette fonction est donc **impure**.  
	Exemple 2 : utilisation d'une boucle  
	```python
	#en impératif
	def somme(liste):
	    """
	    Calcule la somme des éléments de la liste liste.
	    """
	    somme = 0
	    for nbre in liste:
	        somme = somme + nbre
	    return somme
	#En fonctionnel
	def somme(liste):
	    """
	    Calcule la somme des éléments de la liste liste.
	    """
	    if len(liste) == 0:
	        return 0
	    else:
	        return liste[0] + somme(liste[1:])
	```


!!! faq "Programmation fonctionnelle ou non?"
	Ce programme respecte-t-il le paradigme fonctionnel?
	```python
	l = [4,7,3]
	def ajout(i):
	  l.append(i)
	 ```
	 <div id="QCU">
	<div id="enonce_question">
	    Quelle est la bonne réponse ?
	</div><form id="test1">
	    <label><input type="radio" name="test" value="oui"> Oui</label><br>
	    <label><input type="radio" name="test" value="non" > Non</label><br>
	    <input  type="button" style="margin:5px; padding:5px;  background-color : lightblue; border : solid 2px blue; border-radius : 5px;" onclick="reactionQCU1()" value="Vérifer"> 
	    <input id="bouAffQCU1" type="button" onclick="AfficheQCU1()" value="Correction" style="display:none;"><br>
	</form></div>
	        <div id="messageQCU1"></div>
	        <div id="correctionQCU1" style="display:none;"> <p> La bonne réponse est Non car elle modifie une variable exterieure.</p></div>

!!! faq "Programmation fonctionnelle ou non?"
	Ce programme respecte-t-il le paradigme fonctionnel?
	```python
		i = 5
		def fct():
		  if i > 5:
		    return True
		  else :
		    return False
		fct()
	 ```
	 <div id="QCU">
	<div id="enonce_question">
	    Quelle est la bonne réponse ?
	</div><form id="test2">
	    <label><input type="radio" name="test" value="oui"> Oui</label><br>
	    <label><input type="radio" name="test" value="non" > Non</label><br>
	    <input  type="button" style="margin:5px; padding:5px;  background-color : lightblue; border : solid 2px blue; border-radius : 5px;" onclick="reactionQCU2()" value="Vérifer"> 
	    <input id="bouAffQCU2" type="button" onclick="AfficheQCU2()" value="Correction" style="display:none;"><br>
	</form></div>
	        <div id="messageQCU2"></div>
	        <div id="correctionQCU2" style="display:none;"> <p> La bonne réponse est Non car elle modifie une variable exterieure.</p></div>

!!! faq "Programmation fonctionnelle ou non?"
	Ce programme respecte-t-il le paradigme fonctionnel?
	```python
	def mafonction(n):
	    while n<10:
	        print(n)
	        n+=1
	```   
	 <div id="QCU">
	<div id="enonce_question">
	    Quelle est la bonne réponse ?
	</div><form id="test3">
	    <label><input type="radio" name="test" value="oui"> Oui</label><br>
	    <label><input type="radio" name="test" value="non" > Non</label><br>
	    <input  type="button" style="margin:5px; padding:5px;  background-color : lightblue; border : solid 2px blue; border-radius : 5px;" onclick="reactionQCU3()" value="Vérifer"> 
	    <input id="bouAffQCU3" type="button" onclick="AfficheQCU3()" value="Correction" style="display:none;"><br>
	</form></div>
	        <div id="messageQCU3"></div>
	        <div id="correctionQCU3" style="display:none;"> <p> La bonne réponse est Non car elle utilise une boucle `while`.</p></div>

    
Pour toutes les fonctions qui ne respetaient pas le paradigme fonctionnel, vous aurez l'occasion de les modifier lors du TP.

Il existe en python une fonction qui permet de passer une fonction en paramètre d'une autre. Il s'agit de la fonction `eval()`qui permet d'évaluer la valeur d'une chaîne de caractères à condition qu'elle soit évaluable.
Pour une expression : 
```python
print eval("2 + 4")
#6
a = 2
print eval("a == 2")
#true
``` 
Pour une fonction (tester ceci dans un bac à sable et prenez le temps de comprendre ce qu'il se passe) :   
```python
def somme(liste):
    s=0
    for elt in liste:
        s=s+elt
        return s

def moyenne(liste):
    return somme(liste)/len(liste)
    


mesfonctions=['somme','moyenne']

for fct in mesfonctions:
    print(eval(fct+'([2,3,4,5,6])'))
```

## Programmation orientée objet
Je ne reviens pas sur les principe de la POO, cela a déjà été traité en long en large et en travers un peu plus tôt dans l'année. Cela dit le TP nous permettra de l'aborder une nouvelle fois (en diagonale?).  


## Comment choisir son paradigme ?


>Pour simplifier, si votre problème implique une série de manipulations séquentielles simples, suivre le paradigme de programmation impérative de la vieille école serait le moins cher en termes de temps et d'efforts et vous donnerait potentiellement les meilleures performances. 

>Dans le cas de problèmes nécessitant des transformations mathématiques des valeurs, le filtrage des informations, le mappage( transformer une liste en une autre) et les réductions( transformer une liste en une valeur), la programmation fonctionnelle pourrait être adaptée. 

>Si le problème est structuré comme un tas d'objets interdépendants avec certains attributs qui peuvent changer avec le temps, en fonction de certaines conditions, la programmation orientée objet sera certainement la plus naturelle. 

>Bien sûr, il n'y a pas de règle simple, car le choix du paradigme de programmation dépend également fortement du type de données à traiter, des connaissances des programmeurs et de diverses autres choses comme l'évolutivité. 

*source : Perceiving Python programming paradigms*  

Il est a noter que le bon programmeur doit connaître tous ces paradigmes. Certains langages informatiques sont plutôt dédiés à un paradigme ou un autre. Par exemple, le langage `JAVA `est utilisé en POO et `javascript` en évenemetiel. Des langages comme `python` sont polyvalent mais peut etre du coup moins puissants pour certains paradigmes.

<script>
/*-------------------------------------------------------------------------------------------------------*/
/*Question à choix unique*/

function reactionQCU1(){
	var style;
	var msg;
	var reponse = document.getElementById("test1");
	var rep=reponse.elements["test"].value;
	if (rep=="non"){msg='bonne réponse';
	style='style="color:green;"';
	}
	else {msg='mauvaise reponse';
	style='style="color:red;"';
	}
	document.getElementById("messageQCU1").innerHTML='<p '+style+'>'+msg+'</p>';
	document.getElementById("bouAffQCU1").style="margin:5px; padding:5px;  background-color : lightblue; border : solid 2px blue; border-radius : 5px;display:inline;";
}
/*affiche la réponse si on clique sur le bouton correction*/
function AfficheQCU1(){
	document.getElementById("correctionQCU1").style="display:block;";
}

/*-------------------------------------------------------------------------------------------------------*/
/*Question à choix unique*/

function reactionQCU2(){
	var style;
	var msg;
	var reponse = document.getElementById("test2");
	var rep=reponse.elements["test"].value;
	if (rep=="non"){msg='bonne réponse';
	style='style="color:green;"';
	}
	else {msg='mauvaise reponse';
	style='style="color:red;"';
	}
	document.getElementById("messageQCU2").innerHTML='<p '+style+'>'+msg+'</p>';
	document.getElementById("bouAffQCU2").style="margin:5px; padding:5px;  background-color : lightblue; border : solid 2px blue; border-radius : 5px;display:inline;";
}
/*affiche la réponse si on clique sur le bouton correction*/
function AfficheQCU2(){
	document.getElementById("correctionQCU2").style="display:block;";
}

function reactionQCU3(){
	var style;
	var msg;
	var reponse = document.getElementById("test3");
	var rep=reponse.elements["test"].value;
	if (rep=="non"){msg='bonne réponse';
	style='style="color:green;"';
	}
	else {msg='mauvaise reponse';
	style='style="color:red;"';
	}
	document.getElementById("messageQCU3").innerHTML='<p '+style+'>'+msg+'</p>';
	document.getElementById("bouAffQCU3").style="margin:5px; padding:5px;  background-color : lightblue; border : solid 2px blue; border-radius : 5px;display:inline;";
}
/*affiche la réponse si on clique sur le bouton correction*/
function AfficheQCU3(){
	document.getElementById("correctionQCU3").style="display:block;";
}
</script>