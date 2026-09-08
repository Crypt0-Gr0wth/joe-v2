# Chapitre 6 — L'accumulateur de volatilite et la reference dynamique

`updateVolatilityAccumulator` (`PairParameterHelper.sol`) mesure a chaque swap l'ecart entre le bin actif courant et une « reference d'id » (`idReference`) enregistree precedemment : `deltaId = abs(activeId - idReference)`, puis `volAcc = volatilityReference + deltaId * 10000`, plafonne a `maxVolatilityAccumulator` pour eviter que les frais variables n'explosent au-dela d'un seuil raisonnable meme lors d'un mouvement de prix extreme.

`updateReferences` decide, en fonction du temps ecoule depuis la derniere mise a jour (`dt = timestamp - timeOfLastUpdate`), comment faire evoluer cette reference : si `dt` est inferieur a la « periode de filtre » (`filterPeriod`), la reference reste inchangee, ce qui absorbe le bruit des swaps rapproches sans les compter deux fois comme de la volatilite. Au-dela de la « periode de decroissance » (`decayPeriod`), l'accumulateur de volatilite est reduit par le « facteur de reduction » plutot que remis a zero brutalement, un lissage exponentiel qui laisse la commission variable redescendre progressivement apres un pic d'activite plutot que de chuter instantanement.

Ce mecanisme reproduit, entierement on-chain et sans oracle externe, le comportement d'un market maker professionnel qui elargit ses spreads pendant les periodes volatiles et les resserre pendant les periodes calmes — une adaptation dynamique des frais qui n'existe ni dans Uniswap v2 (frais fixes) ni, sous cette forme precise, dans Uniswap v3 (frais fixes par pool selon un tier choisi a la creation).

[Chapitre suivant : LBFactory et le deploiement par clone immuable](07-factory.md)
