# Chapitre 13 — Limites connues et perimetre de ce parcours

Le code de Liquidity Book (Joe V2) est publie sous licence MIT (`LICENSE`), une licence permissive standard sans restriction d'usage particuliere.

Ce parcours ne couvre pas en detail les interfaces de compatibilite avec l'ancienne version Trader Joe v1 (`ILBLegacyFactory.sol`, `ILBLegacyRouter.sol`, `ILBLegacyPair.sol`, `ILBLegacyToken.sol`, `IJoeFactory.sol`, `IJoePair.sol`), le detail complet des types point-fixe de bas niveau (`Uint128x128Math.sol`, `Uint256x256Math.sol`, `PackedUint128Math.sol`, `Encoded.sol`, `BitMath.sol`, `SafeCast.sol`), ni les scripts de deploiement (`script/`). Le contrat `LBBaseHooks.sol` fournit une base pour ecrire des hooks personnalises mais aucune implementation concrete de hook n'est incluse dans ce depot.

Rien n'a ete installe, compile, deploye ni execute pour ecrire ces chapitres. Aucun test n'a ete lance ; ces chapitres decrivent ce que le code Solidity dit faire, en renvoyant aux fichiers cites. Le depot fournit sa propre suite de tests Foundry (dossier `test/`) pour verification independante.
