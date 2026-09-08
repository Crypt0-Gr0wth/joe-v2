# Chapitre 5 — PairParameterHelper : l'etat compact de la paire en un seul mot de stockage

`PairParameterHelper.sol` (440 lignes) encode l'integralite des parametres dynamiques et statiques d'une paire dans un unique `bytes32`, decoupe en 13 champs de largeurs variables (documente en commentaire dans le fichier) : facteur de base, periode de filtre, periode de decroissance, facteur de reduction, controle de la commission variable, part protocole, accumulateur de volatilite (courant et maximum), reference de volatilite, reference d'id, horodatage de derniere mise a jour, index d'oracle et id actif — soit 256 bits utilises presque integralement, un seul `SLOAD`/`SSTORE` pour lire ou ecrire l'etat complet de la paire a chaque operation.

Cet encodage compact sert directement au calcul des frais dynamiques : `getBaseFee` multiplie simplement le facteur de base par le `binStep`, tandis que `getVariableFee` eleve au carre l'accumulateur de volatilite multiplie par le `binStep` avant de le ponderer par le controle de commission variable — une commission qui croit donc de facon quadratique avec la volatilite recente, penalisant fortement les periodes de forte activite de prix pour compenser le risque accru des fournisseurs de liquidite.

[Chapitre suivant : l accumulateur de volatilite et la reference dynamique](06-volatilite.md)
