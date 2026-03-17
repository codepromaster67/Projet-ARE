# Projet ARE
**Maxim**

code ajouté


eojfhziufdhqpdsifhqoisd

#Cas n°1 aucune regulation ni intervation


#variables exogènes
indice0 = 1
population = 1000
titres = 25
res = [indice0]
matrice = [[0.7, 0.2, 0.1], 
           [0.3, 0.4, 0.3], 
           [0.1, 0.2, 0.7]]
ancienetat = 1


vecteurpopulation = np.random.normal(0.5, 0.15, population) 
# vecteur contenant toutes les opinions de la population, aux extremes on a des gens qui investissent beaucoup ou peu les valeurs sont comprises entre 0 et 1

vecteurindice = np.array([np.random.uniform(-1/4, 3/4)*10 for _ in range(titres)])
#vecteur contenant tous les indices de prix

def passage(matrice, etat):
    k = np.random.uniform()
    if k <matrice[etat][0]:
        etat =0
    else:
        if k < matrice[etat][0] + matrice[etat][1] and k >= matrice[etat][0]:   
            etat = 1
        else:
            etat = 2
    return etat


def probapopulation(etat, vecteurpopulation):
    vecteur = []
    if etat == 0:
        return vecteurpopulation * 0.8
    if etat == 1:
        return vecteurpopulation
    if etat == 2: 
        for e in vecteurpopulation:
            if e*1.2<1:
               vecteur.append(e*1.2)
            else:
                vecteur.append(1)
        return np.array(vecteur)
    

def prop_investisseurs(etat):
    vecteur_investisseurs = []
    if etat == 2:
        vecteur_investisseurs = np.array([e for e in vecteurpopulation if e > 0.4])
    if etat == 1:
        vecteur_investisseurs = np.array([e for e in vecteurpopulation if e > 0.5])
    if etat == 0:
        vecteur_investisseurs = np.array([e for e in vecteurpopulation if e > 0.6])
    
    return vecteur_investisseurs


def calculer_indice(vecteurindice, vecteur_investisseurs, etat, liste):
    res = 0
    for i in range(len(vecteurindice)):
        res = 0
        if etat == 0:
            res =0
            for inv in vecteur_investisseurs:
                res = res + np.random.normal(-0.03, 0.001)
            vecteurindice[i] += res

        if etat == 2:
            for inv in vecteur_investisseurs:
                res = res + np.random.normal(0.05, 0.001)
            vecteurindice[i] += res   

        if etat == 1:
            for inv in vecteur_investisseurs:
                res = res + np.random.normal(0, 0.001)
            vecteurindice[i] += res
    nv_indice = np.mean(vecteurindice) 
    liste.append(nv_indice)
    return nv_indice
            


def probamatrice(matrice,etat, indice1, indice0, epsilon):
    variation = (indice1 -indice0)/100

    if variation > 0:
        for i in range(len(matrice[etat])):
            matrice[etat][i] = 1  #provisoire a changer

    if abs(variation)<epsilon:
        for i in range(len(matrice[etat])):
            matrice[etat][i] = 1   #a cahnger

    else:
        for i in range(len(matrice[etat])):
            matrice[etat][i] = 1        #a changer

    return matrice
