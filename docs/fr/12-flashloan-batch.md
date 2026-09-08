# Chapitre 12 — Les emprunts flash et les operations de liquidite en lot sur plusieurs bins

`LBPair` expose un emprunt flash standard (documente via `ILBFlashLoanCallback.sol`), gouverne par les crochets `BEFORE_FLASH_LOAN_FLAG`/`AFTER_FLASH_LOAN_FLAG` du chapitre 9 lorsqu'un contrat de hook est attache a la paire — l'emprunteur recoit les jetons demandes, execute sa logique via un callback, et le contrat verifie que le solde a ete restaure avec les frais dus avant la fin de la transaction, le meme motif que tout emprunt flash standard mais avec le crochet optionnel intercale.

Fournir de la liquidite sur plusieurs bins en une seule transaction est une operation centrale de l'experience utilisateur de Liquidity Book, puisque la strategie typique d'un fournisseur consiste a repartir sa liquidite sur une plage de bins autour du prix courant plutot que sur un seul. `LiquidityConfigurations.sol` (`src/libraries/math/`) encode, pour chaque bin cible d'un depot en lot, la distribution relative de jeton X et de jeton Y a y apporter — une configuration compacte qui permet de decrire en un seul appel une strategie de repartition de liquidite complexe (par exemple une distribution uniforme, ou concentree pres du prix courant) sans transaction separee par bin.

Le retrait fonctionne symetriquement : un utilisateur peut bruler ses parts dans plusieurs bins en une seule transaction groupee, ce qui reduit significativement le cout en gas par rapport a des retraits individuels bin par bin.

[Chapitre suivant : limites et perimetre](13-limites-et-perimetre.md)
