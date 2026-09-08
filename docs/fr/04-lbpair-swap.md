# Chapitre 4 — LBPair et le parcours de l'arbre de bins actifs pendant un swap

`LBPair.sol` (1114 lignes) orchestre le swap complet : partant du bin actif courant (`activeId`, stocke dans les parametres compacts de la paire, chapitre 5), le contrat consomme la liquidite disponible dans ce bin puis, si le montant du swap n'est pas entierement satisfait, se deplace vers le bin suivant dans la direction du swap.

Ce deplacement entre bins n'est pas un simple incrementement lineaire d'id, car la plupart des bins d'une paire sont vides — la majorite de l'espace des prix possibles n'a jamais recu de liquidite. `TreeMath.sol` (230 lignes) resout ce probleme avec une structure arborescente a trois niveaux (`level0`, `level1`, `level2`, chacun un `mapping` de bits `bytes32`) qui permet de trouver le prochain bin non vide dans une direction donnee en temps quasi constant plutot qu'en parcourant sequentiellement des milliers de bins vides. Chaque bit de `level2` signale la presence de liquidite dans un bin precis ; `level1` et `level0` agregent cette information par blocs de 256, permettant de sauter directement aux zones denses en liquidite.

Ce mecanisme d'arbre de bits est ce qui rend Liquidity Book praticable malgre son espace de prix theoriquement immense (`uint24`, plus de 16 millions de bins possibles par paire) : sans lui, localiser le prochain bin actif serait prohibitif en gas des que la liquidite est dispersee.

[Chapitre suivant : PairParameterHelper, l etat compact de la paire](05-pairparameters.md)
