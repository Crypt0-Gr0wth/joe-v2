# Chapitre 7 — LBFactory et le deploiement par clone immuable des paires

`LBFactory.sol` (756 lignes) est a la fois le registre de toutes les paires deployees et le point d'entree pour en creer de nouvelles. Sauf si `creationUnlocked` est active, seul le proprietaire de la fabrique peut deployer une nouvelle paire — une restriction deliberee par rapport aux fabriques permissionless d'Uniswap, justifiee par la complexite des parametres de frais dynamiques (chapitre 5 et 6) qui doivent etre choisis avec soin pour chaque nouvelle paire.

Le deploiement effectif passe par `ImmutableClone.sol` (252 lignes), une bibliotheque de clonage minimaliste inspiree de Solady et du motif « clones with immutable args » : plutot que d'utiliser un proxy classique avec stockage mutable, chaque paire deployee est un clone dont les parametres immuables (adresses des deux jetons, `binStep`) sont encodes directement dans le bytecode du clone lui-meme, accessibles via `CODECOPY` a l'execution — evitant ainsi tout acces au stockage pour lire ces valeurs constantes, exactement le meme objectif de reduction de cout que le motif meta-proxy documente pour l'Euler Vault Kit ailleurs dans cette bibliotheque, mais implemente ici sans passer par le calldata.

La fabrique maintient egalement des « presets » de parametres de frais reutilisables pour un `binStep` donne, permettant de standardiser les parametres de risque entre plusieurs paires partageant le meme profil de volatilite plutot que de les configurer individuellement a chaque creation.

[Chapitre suivant : LBToken, le standard de parts par bin](08-lbtoken.md)
