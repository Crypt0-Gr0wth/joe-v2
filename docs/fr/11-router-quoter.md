# Chapitre 11 — LBRouter et LBQuoter : l'interface utilisateur securisee et le routage optimal

`LBRouter.sol` (1149 lignes, le plus long fichier du depot) est le contrat avec lequel la plupart des utilisateurs interagissent directement plutot qu'avec `LBPair` : le README precise explicitement que « most users shouldn't interact directly with the pair », le routeur ajoutant les verifications de securite standard d'un routeur AMM — deadlines de transaction, montants minimums recus, verification que les jetons effectivement recus correspondent aux jetons attendus (protection contre les jetons a re-basage ou a frais de transfert non annonces).

`LBQuoter.sol` (520 lignes) resout un probleme specifique a l'architecture multi-bin de Liquidity Book : contrairement a un pool Uniswap v2 unique par paire, une route optimale peut necessiter de traverser plusieurs bins consecutifs dont les prix different legerement, et potentiellement plusieurs paires distinctes pour un swap multi-hop. `LBQuoter` simule ce parcours hors execution reelle pour renvoyer la meilleure route parmi plusieurs candidates fournies, une etape recommandee avant tout swap pour garantir le meilleur taux de change effectif compte tenu de la fragmentation de la liquidite entre bins.

Le routeur maintient egalement une compatibilite explicite avec les anciennes paires Trader Joe v1 de type Uniswap v2 classique (`IJoeRouter01`, `IJoeRouter02`, `IJoePair`, `ILBLegacyRouter`, `ILBLegacyPair`), permettant a un utilisateur de router un swap a travers l'ancien et le nouveau systeme de facon transparente selon la meilleure liquidite disponible.

[Chapitre suivant : les emprunts flash et les operations en lot](12-flashloan-batch.md)
