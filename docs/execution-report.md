# Rapport d'exécution

Campagne du 12/10/2026 sur QuickOrder V3.1 (commit `d4606da`), en local avec Docker, base de démo remise à zéro avant de commencer.

## Résultats

| Type de cas | Tests | Pass | Fail | Blocked | Skipped |
|---|---|---|---|---|---|
| Cas nominal | 6 | 6 | 0 | 0 | 0 |
| Cas limite | 6 | 3 | 3 | 0 | 0 |
| Cas d'erreur | 6 | 2 | 3 | 1 | 0 |
| Règle métier | 6 | 0 | 6 | 0 | 0 |
| Total | 24 | 11 (46 %) | 12 (50 %) | 1 (4 %) | 0 |

Le test bloqué est TC-PAIE-002, le simulateur de paiement ne permet pas de refuser une carte.

Tous les cas nominaux passent, l'application marche quand on suit le parcours prévu. Les échecs viennent des règles métier et des contrôles côté serveur, qui manquent sur le site comme dans l'API.

## Bugs

| Bug | Titre | Sévérité | Priorité |
|---|---|---|---|
| [BUG-01](bug-reports/BUG-01-paypal-double-commande.md) | Un paiement PayPal crée deux commandes identiques | Critique | Haute |
| [BUG-02](bug-reports/BUG-02-especes-montant-insuffisant.md) | Une commande en espèces est validée avec un montant inférieur au total | Critique | Haute |
| [BUG-03](bug-reports/BUG-03-restaurant-ferme-commandable.md) | Un restaurant fermé reçoit quand même des commandes | Majeure | Haute |
| [BUG-04](bug-reports/BUG-04-stock-non-controle.md) | Les produits épuisés restent commandables et le stock devient négatif | Majeure | Haute |
| [BUG-05](bug-reports/BUG-05-minimum-commande-ignore.md) | Le minimum de commande n'est pas appliqué | Majeure | Haute |
| [BUG-06](bug-reports/BUG-06-adresse-vide-nouveau-compte.md) | Un nouveau compte peut commander sans adresse de livraison | Majeure | Haute |
| [BUG-07](bug-reports/BUG-07-api-coupon-expire-accepte.md) | L'API accepte un coupon expiré lors de la création d'une commande | Majeure | Haute |
| [BUG-08](bug-reports/BUG-08-atlas15-remise-10-pourcent.md) | Le coupon ATLAS15 annoncé à -15 % n'applique que -10 % | Majeure | Haute |
| [BUG-09](bug-reports/BUG-09-redirection-externe-login.md) | Après la connexion, le paramètre next peut renvoyer vers un autre site | Majeure | Haute |
| [BUG-10](bug-reports/BUG-10-filtre-livraison-inverse.md) | Le filtre Livraison max affiche les restaurants les plus chers | Mineure | Moyenne |
| [BUG-11](bug-reports/BUG-11-api-erreur-500.md) | L'API plante avec une erreur 500 si product_id est envoyé en texte | Mineure | Moyenne |

## Principaux risques

- Le client peut payer deux fois avec PayPal, et une commande en espèces passe pour payée même s'il manque de l'argent.
- Des commandes payées ne pourront pas être livrées (restaurant fermé, produit épuisé, adresse vide, montant sous le minimum).
- Les promotions ne sont pas fiables, avec ATLAS15 à 10 % au lieu de 15 % et un coupon expiré accepté par l'API.
- Un lien de connexion piégé peut envoyer le client vers un autre site.

## Recommandation

No-Go. Les deux bugs critiques et six des bugs majeurs touchent le paiement, la commande et les coupons, qui sont les parcours les plus critiques. S'y ajoute une faille de redirection sur la connexion. Avant de revoir la décision, il faut corriger les bugs de priorité haute (BUG-01 à BUG-09), puis rejouer les 12 cas en échec et vérifier que les 11 cas qui passaient passent toujours.

## Remarques

Le lancement avec Docker ne marche pas tel quel sur macOS. Le port 5000 est déjà pris par AirPlay et `docker-entrypoint.sh` n'est pas exécutable. Je l'ai contourné avec un fichier de surcharge Docker Compose, sans toucher au code. La commande `pytest -q` indiquée dans le README du projet ne démarre pas non plus.
