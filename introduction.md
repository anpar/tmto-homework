# Introduction
Dans cette section, on introduit la notion de compromis temps-mémoire (ou time-memory trade-off, TMTO en anglais)
de manière intuitive, via des exemples. Les sections
suivantes s'intéresseront quant à elle à la description du fonctionnement d'algorithmes classiques permettant de mettre
en oeuvre un compromis temps-mémoire.

## Objectif d'un compromis temps-mémoire
On se place ici dans le dispositif habituel dans lequel Alice veut envoyer un message *m* à Bob de façon sécurisée.
Pour ce faire, on suppose que Alice et Bob ont déjà eu l'occasion de s'échanger une clé secrète *k* leur permettant de
communiquer de façon sécurisée en utilisant leur algorithme de chiffrement favori. Nous allons ici jouer le rôle du méchant,
Eve, dont le but est de pouvoir, d'une manière ou d'une autre, décrypter les messages que s'envoient Bob et Alice. Eve ne
peut cependant observer que des messages chiffrés *c = Enc(k,m)* où *Enc* représente l'algorithme de chiffrement préféré
d'Alice et Bob. Le seul moyen de déchiffrer un tel message est de connaître la clé secrète *k*, *m = Dec(k,c)* où *Dec*
représente l'algorithme de déchiffrement.

Admettons maintenant que, d'une manière ou d'une autre, Eve parvienne à obtenir le chiffrement d'un message *m'* choisi.
Un tel type d'attaque, appellée "attaque à texte clair choisi" (ou choosen-plaintext attack en anglais), peut sembler
irréaliste à première vue: comment Eve pourrait-elle convaincre Bob ou Alice de chiffrer un message pour elle? Et pourtant, de
nombreux exemples de telles attaques existent. Le plus connu est peut-être [celui-ci](http://www.slate.com/blogs/quora/2013/11/20/u_s_in_world_war_ii_how_the_navy_broke_japanese_codes_before_midway.html).
Eve est donc maintenant en possession de *c' = Enc(k, m')*. A partir de là, il devient possible pour Eve d'essayer de trouver
la clé secrète partagée entre Alice et Bob. Une première idée serait de simplement procéder à une recherche exhaustive sur
toutes les clés *k* et de vérifier si *Enc(k, m') = c'* pour chacune de ces clés. Un tel algorithme nécessiterait cependant,
dans le pire des cas, autant d'étapes qu'il y a de clés possibles. Si il y a *N* clés *k*, cela fait *N* possibilités
à explorer. Notons néanmoins que cette approche ne requiert **aucune mémoire**.

Une deuxième approche à ce problème serait de précalculer *c = Enc(k, m')* pour toutes les clés *k* possibles et de stocker
les résultats dans une énorme table indexée par *c* et dont chaque ligne contiendrait *k* la clé correspondante. On procède
ensuite de la même façon que précedemment. Eve, d'une manière ou d'une autre, parvient à obtenir le chiffrement de *m'* :
*c' = Enc(k, m')*. Tout ce qu'il lui reste à faire ensuite est d'aller chercher dans la table qu'elle a stockée en mémoire
la clé *k* correspondant au chiffrement *c'* de *m'*. Cette approche diffère de la précédente en deux points. Premièrement,
l'attaque nécessite une étape de **pré-calcul** qui nécessite à nouveau, dans le cas d'une clé contenant
*N* étapes. En plus de cela, cette approche nécessite une mémoire assez grande pour stocker entièrement la table
de correspondante entre chiffrés et clés. Jusqu'ici, on serait tenter de dire que cette approche n'a aucun intèrêt puisqu'en
plus d'utiliser *N* étapes comme l'approche précédente, il nous faut une mémoire permettant de stocker une table de *N*
lignes. Cependant, cette méthode a pour avantage de s'éxécuter ensuite en **temps constant**. Cette approche n'a du sens
que si l'on doit faire plusieurs attaques (sinon, autant directement utiliser la première approche et économiser *N*
lignes de mémoires), cela permet d'amortir le coût de pré-calcul.

Un problème de taille demeure cependant. Une taille de clé typique pour un chiffrement à clé symétrique est 128 bits. Cela
signifie que *N*, le nombre total de clés, vaut 2^128 = 3.4e38. Aucun ordinateur à l'heure actuelle (et probablement pour
très longtemps encore) n'est capable de faire un recherche exhaustive sur un espace d'une telle taille, et encore moins
de stocker une table contenant 2^128 lignes en mémoire... C'est là qu'intervient le compromis temps-mémoire qui, comme son
nom l'indique, vise à trouver un juste milieu entre temps d'exécution et mémoire utilisée.

D'autres exemples de TMTO (pas seulement dans le domaine de la cryptanalyse) sont présentés dans [cet article]
(http://www.cs.sjsu.edu/faculty/stamp/RUA/TMTO.pdf).
