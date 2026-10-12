# Plan d'amélioration

| Priorité | Amélioration | Pourquoi |
|---|---|---|
| 1. Haute | Créer une seule commande par paiement PayPal et refuser une commande en espèces si le montant remis est inférieur au total | Corrige BUG-01 et BUG-02, les deux bugs critiques. Le client ne doit jamais payer deux fois ni passer pour payé à tort. |
| 2. Haute | Vérifier côté serveur, sur le site et dans l'API, que le restaurant est ouvert, que le stock suffit, que le minimum est atteint et que l'adresse est complète avant de valider une commande | Corrige BUG-03 à BUG-06, qui ont la même cause. Un seul contrôle partagé évite que le site et l'API divergent. |
| 3. Haute | Appliquer les mêmes règles de coupon partout (expiration comprise dans l'API) et aligner ATLAS15 sur l'offre affichée | Corrige BUG-07 et BUG-08. Une réduction affichée doit être celle appliquée. |
| 4. Haute | N'accepter qu'une adresse interne au site dans le paramètre next de la connexion | Corrige BUG-09, qui peut servir à du phishing. Correction de quelques lignes. |
| 5. Moyenne | Renvoyer des erreurs en JSON avec le bon code (400 plutôt que 500) et corriger le filtre de livraison | Corrige BUG-10 et BUG-11. |
| 6. Moyenne | Rendre l'installation Docker fonctionnelle, réparer `pytest` et ajouter un test automatique pour chaque bug corrigé | Permet de revalider les corrections et d'éviter que les bugs reviennent. Ajouter aussi un cas de paiement refusé au simulateur pour pouvoir exécuter TC-PAIE-002. |
