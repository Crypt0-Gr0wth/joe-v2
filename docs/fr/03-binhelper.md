# Chapitre 3 — BinHelper : le calcul des parts de liquidite et le swap sans slippage intra-bin

`BinHelper.sol` (367 lignes) contient les fonctions qui traduisent les reserves d'un bin en parts de liquidite et vice-versa. `getSharesAndEffectiveAmountsIn` calcule combien de parts un fournisseur de liquidite recoit pour un depot donne : si le bin est vide, les parts recues sont la racine carree de la liquidite apportee (`userLiquidity.sqrt()`, motif emprunte a Uniswap v2 pour eviter une manipulation triviale au premier depot) ; sinon, les parts sont proportionnelles a la liquidite existante du bin (`shares = userLiquidity * totalSupply / binLiquidity`).

La fonction retourne egalement un « effectiveAmountsIn » qui peut etre inferieur au montant demande : si le ratio des deux jetons apportes ne correspond pas exactement a la composition courante du bin, seule la part effectivement utilisable est acceptee, le reste restant dans le solde de l'utilisateur plutot que d'etre force dans le bin a un ratio incorrect.

A l'interieur d'un bin donne, un swap se comporte comme une simple formule a somme constante sans aucune courbure : tant que le swap reste dans un seul bin, il n'y a litteralement aucun slippage — chaque unite de jeton X echangee rapporte toujours le meme nombre d'unites de jeton Y, au prix fixe du bin. Le slippage n'apparait que lorsque le volume du swap epuise un bin et doit continuer dans le bin suivant (chapitre 4), a un prix legerement different.

[Chapitre suivant : LBPair et le parcours de l arbre de bins actifs](04-lbpair-swap.md)
