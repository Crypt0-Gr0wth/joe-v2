# Chapitre 9 — Hooks : l'extension programmable des paires avant et apres chaque operation

`Hooks.sol` (370 lignes) definit un systeme de crochets binaires similaire en esprit aux hooks d'Uniswap v4 : dix indicateurs (`BEFORE_SWAP_FLAG`, `AFTER_SWAP_FLAG`, `BEFORE_FLASH_LOAN_FLAG`, `AFTER_FLASH_LOAN_FLAG`, `BEFORE_MINT_FLAG`, `AFTER_MINT_FLAG`, `BEFORE_BURN_FLAG`, `AFTER_BURN_FLAG`, `BEFORE_TRANSFER_FLAG`, `AFTER_TRANSFER_FLAG`) sont encodes comme des bits individuels dans un `bytes32` qui contient aussi l'adresse du contrat de hook, permettant d'activer selectivement seulement les crochets pertinents pour une paire donnee sans surcout pour les operations non concernees.

Un contrat de hook externe (`ILBHooks`, implemente separement de ce depot) peut ainsi injecter de la logique personnalisee avant ou apres un swap, un depot, un retrait ou un transfert — par exemple pour appliquer des frais additionnels, mettre a jour un oracle externe, ou restreindre l'acces a certains utilisateurs. `LBBaseHooks.sol` fournit une implementation de reference abstraite que les integrateurs peuvent heriter plutot que de reimplementer l'interface complete depuis zero.

Ce systeme place Liquidity Book parmi les rares AMM en production a offrir une extensibilite programmable de ce type des avant la generalisation du motif hooks popularise plus tard par Uniswap v4.

[Chapitre suivant : OracleHelper, l oracle de prix on-chain circulaire](10-oracle.md)
