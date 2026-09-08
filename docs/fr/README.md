# Parcours francais de Liquidity Book (Trader Joe v2) — Swap par bins

Lecture commentee de l'AMM Liquidity Book de Trader Joe, en francais, un mecanisme par chapitre.
Aucun code n'a ete installe, compile ni execute : ce parcours est purement documentaire.

1. [Presentation de Liquidity Book](01-presentation.md)
2. [PriceHelper : le prix constant par bin et le bin step](02-pricehelper.md)
3. [BinHelper : le calcul des parts de liquidite et le swap sans slippage intra-bin](03-binhelper.md)
4. [LBPair et le parcours de l'arbre de bins actifs pendant un swap](04-lbpair-swap.md)
5. [PairParameterHelper : l'etat compact de la paire en un seul mot de stockage](05-pairparameters.md)
6. [L'accumulateur de volatilite et la reference dynamique](06-volatilite.md)
7. [LBFactory et le deploiement par clone immuable des paires](07-factory.md)
8. [LBToken : le standard de parts par bin, proche ERC-1155 sans callback](08-lbtoken.md)
9. [Hooks : l'extension programmable des paires avant et apres chaque operation](09-hooks.md)
10. [OracleHelper : l'oracle de prix on-chain a tampon circulaire](10-oracle.md)
11. [LBRouter et LBQuoter : l'interface utilisateur securisee et le routage optimal](11-router-quoter.md)
12. [Les emprunts flash et les operations de liquidite en lot sur plusieurs bins](12-flashloan-batch.md)
13. [Limites connues et perimetre de ce parcours](13-limites-et-perimetre.md)
