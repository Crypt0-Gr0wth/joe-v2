# Chapitre 10 — OracleHelper : l'oracle de prix on-chain a tampon circulaire

`OracleHelper.sol` (278 lignes) implemente un oracle de prix similaire dans son principe a celui d'Uniswap v3 : chaque swap peut ecrire un nouvel echantillon (`sample`) dans un tampon circulaire dont la taille est configurable par paire, permettant a des contrats tiers de calculer un prix moyen pondere dans le temps (TWAP) resistant a la manipulation instantanee.

`SampleMath.sol` (199 lignes) encode chaque echantillon de facon compacte : horodatage cumulatif, id actif cumulatif et volatilite accumulee cumulative, tous stockes dans un seul `bytes32` par slot d'echantillon. Le fait de stocker des valeurs cumulatives plutot que des valeurs instantanees permet a un lecteur externe de calculer une moyenne sur n'importe quelle fenetre temporelle passee couverte par le tampon, en soustrayant simplement deux echantillons cumulatifs et en divisant par l'ecart de temps entre eux — la meme technique que l'oracle geometrique d'Uniswap v3, mais applique ici a l'id de bin plutot qu'au tick.

L'index d'oracle courant (`oracleId`, stocke dans les parametres compacts de la paire, chapitre 5) pointe vers la position d'ecriture suivante dans le tampon circulaire ; une fois le tampon plein, chaque nouvel echantillon ecrase le plus ancien, sauf si la taille du tampon a ete explicitement agrandie par la gouvernance de la paire.

[Chapitre suivant : LBRouter et LBQuoter, l interface utilisateur securisee](11-router-quoter.md)
