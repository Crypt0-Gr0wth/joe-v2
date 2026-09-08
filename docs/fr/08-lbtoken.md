# Chapitre 8 — LBToken : le standard de parts par bin, proche ERC-1155 sans callback

`LBToken.sol` (261 lignes) represente la part de liquidite qu'un utilisateur detient dans chaque bin individuel d'une paire, ou l'id du bin (chapitre 2) sert directement d'identifiant de jeton — une structure multi-token naturelle puisqu'un fournisseur de liquidite peut detenir des parts dans un grand nombre de bins simultanement au sein d'une seule paire.

Le README du depot precise explicitement le choix de conception : LBToken ressemble a ERC-1155 dans sa forme (soldes multiples par id, transferts en lot) mais omet deliberement les callbacks `onERC1155Received`/`onERC1155BatchReceived` « pour des raisons de securite » — ces callbacks, dans ERC-1155 standard, permettent a un contrat destinataire d'executer du code arbitraire pendant un transfert, une surface de reentrance que Liquidity Book choisit d'eliminer completement plutot que de la neutraliser par des gardes de reentrance supplementaires. Le standard omet egalement toute fonction ou variable relative a ERC-721, LBToken n'ayant pas vocation a representer des positions non fongibles individuelles comme le fait le NFT de position d'Uniswap v3.

[Chapitre suivant : Hooks, l extension programmable des paires](09-hooks.md)
