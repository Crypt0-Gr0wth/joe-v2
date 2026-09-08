# Chapitre 1 — Presentation de Liquidity Book

Liquidity Book (LB) est l'AMM de Trader Joe, fonde sur un modele radicalement different des courbes continues de type Uniswap v2/v3 : la liquidite n'est pas repartie sur une courbe mathematique mais organisee en « bins » (casiers) discrets, chacun a un prix fixe et constant. A l'interieur d'un bin, un swap se comporte comme une simple somme constante (x + y = k), sans slippage — le slippage n'apparait qu'au passage d'un bin a l'autre. C'est ce qui permet a LB d'offrir des swaps a frais nuls a l'interieur d'un bin unique, une propriete que ni Uniswap v2 (courbe x*y=k continue) ni Uniswap v3 (courbe concentree mais toujours continue par tick) ne peuvent reproduire exactement.

Le contrat central est `LBPair.sol` (1114 lignes), qui contient toute la logique de swap, d'ajout et de retrait de liquidite, jamais deploye directement mais toujours via la fabrique `LBFactory.sol`. Les parts de liquidite d'un utilisateur dans un bin sont representees par `LBToken.sol`, un standard proche d'ERC-1155 mais deliberement depourvu de callbacks (pour des raisons de securite) et de tout ce qui touche a ERC-721.

Ce parcours s'appuie sur le depot clone a la date d'ecriture, branche `main`. Fichiers centraux : `src/LBPair.sol`, `src/LBFactory.sol`, `src/LBToken.sol`, `src/libraries/BinHelper.sol`, `src/libraries/PriceHelper.sol`, `src/libraries/PairParameterHelper.sol`, `src/libraries/FeeHelper.sol`, `src/libraries/OracleHelper.sol`, `src/libraries/Hooks.sol`, `src/libraries/ImmutableClone.sol` et `src/libraries/math/TreeMath.sol`.

Rien n'a ete installe, compile ni execute pour ecrire ces chapitres.

[Chapitre suivant : PriceHelper, le prix constant par bin](02-pricehelper.md)
