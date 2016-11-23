# Introduction
Dans cette section, on introduit la notion de compromis temps-mémoire de manière intuitive, via des exemples. Les sections
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
dans le pire des cas, autant d'étapes qu'il y a de clés possibles. Si la clé *k* contient 80 bits, cela fait 2^80 possibilités
à explorer. Notons néanmoins que cette approche ne requiert **aucune mémoire** (mais requiert par contre énormément de temps).

Une deuxième approche à ce problème 
