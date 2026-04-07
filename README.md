# Projet ARE
POUR MAXIM LE CODE DE CALCULINDICE:

def calculer_indice(vecteurindice, vecteur_investisseurs, etat):
    res = 0
    for i in range(len(vecteurindice)):
        res = 0
        if etat == 0:
            for inv in vecteur_investisseurs:
                res = res - np.random.normal(0.002, 0.00001)
            vecteurindice[i] += res
    
        if etat == 2:
            for inv in vecteur_investisseurs:
                res = res + np.random.normal(0.001, 0.00001)
            vecteurindice[i] += res

        if etat == 1:
            for inv in vecteur_investisseurs:
                res = res + np.random.normal(0, 0.00001)
            vecteurindice[i] += res
        
        if vecteurindice[i] < 0.01:
            vecteurindice[i] = 0.01

    nv_indice = np.mean(vecteurindice) 
    return nv_indice


il faudra changer le vecteur indice, en fait c'est un vecteur prix et l'indice c'est la moyenne de ces prix


autres idées de changements:

1)evenements aléatoires:
-guerres(en cours par Paul)
-virus(en cours par Paul) 
...
ces evenements impactent fortement le marché, ça pourrait etre intéressant de voir leurs effets et conséquences

2)Asymetrie d'information:
certaines personnes connaissent en avance les probabilités de la matrice et peuvent donc prédire le comportement du marché, cette idée est plus dure donc on privilegiera les précedentes

Bibliographie Générale : 

Publication qui a inspiré le projet de recherche : 

https://www.academia.edu/download/116465685/8139.pdf

Utilisation des chaînes de Markov : 

https://fr.wikipedia.org/wiki/Chaîne_de_Markov

https://www.youtube.com/watch%3Fv%3De0ZHDK4DSEI&ved=2ahUKEwjIno3uj9qTAxWuQ6QEHT1xNNIQwqsBegQIRRAB&usg=AOvVaw1wYoZSkpzwtxGyJrznJbPq

https://www.bibmath.net/dico/index.php?action=affiche&quoi=./m/markov.html

Implémentation informatique : 

Python : https://www.python.org

Numpy : https://numpy.org

Matplotlib : https://matplotlib.org

Bibliographie cas par cas : 

Bibliographie pour le cas 3 : Choc instantané (appelé Black Swan Theory)

 https://en.wikipedia.org/wiki/Black_swan_theory

