# Le compromis temps-mémoire de Hellman
En 1980, Martin E. Hellman propose un compromis temps-mémoire dans un article intitulé [A cryptanalytic Time-Memory Trade-Off]
(http://www.cs.miami.edu/home/burt/learning/Csc609.102/doc/36.pdf). Cette section explique le principe de fonctionnement
de ce TMTO.

Dans son article, Martin E. Hellman propose un TMTO dans le même contexte que celui de l'introduction. Le but est donc
de retrouver la clé *k* utilisée par Alice et Bob pour communiquer secrètement. Pour ce faire, on procède à nouveau à une
attaque à texte clair choisi. Cette section décrit le TMTO de Martin E. Hellman dans 2 situations différentes 
- Dans un monde parfait où tout se passe le plus idéalement possible ;
- Dans un cas réel, avec l'algorithme DES (Data Encryption Standard).

## Dans un monde parfait...
Imaginons dans un premier temps un algorithme de chiffrement par bloc opérant sur des blocs de 64 bits (en entré et en sortie)
avec une clé de 64 bits également. L'espace des messages chiffrés *C* et l'espace des clés *K* sont donc identiques et c'est
justement cela qu'exploite Hellman pour construire son TMTO. Comme *C* et *K* sont identiques, le chiffrement d'un message
*m* par une clé *k*, *c = Enc(k,m)*, peut lui même être considéré comme une clé. L'idée d'Hellman est donc de construire
des chaînes de chiffrement du message choisi *m* en utilisant en guise de clé le chiffrement précédent. Plus formellement,
