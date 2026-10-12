# Matrice risque × impact

Le risque correspond à la probabilité qu'il y ait un défaut (beaucoup de règles, deux points d'entrée avec le site et l'API). L'impact correspond à la conséquence pour le client ou pour l'entreprise.

| Parcours | Risque | Impact | Priorité de test |
|---|---|---|---|
| Paiement | Élevé | Élevé | 1 |
| Passage de commande | Élevé | Élevé | 1 |
| Coupons | Élevé | Moyen | 2 |
| API | Élevé | Moyen | 2 |
| Panier et stock | Moyen | Élevé | 2 |
| Connexion | Moyen | Élevé | 2 |
| Suivi de commande | Moyen | Moyen | 3 |
| Recherche et filtres | Moyen | Faible | 4 |
| Profil, avis, favoris | Faible | Faible | Hors périmètre |

| Risque \ Impact | Faible | Moyen | Élevé |
|---|---|---|---|
| Élevé | | Coupons, API | Paiement, passage de commande |
| Moyen | Recherche et filtres | Suivi de commande | Panier et stock, connexion |
| Faible | Profil, avis, favoris | | |

Après la campagne, les deux bugs critiques sont sur le paiement, dans la case en haut à droite, et tous les bugs de priorité haute sont sur des parcours de priorité 1 ou 2.
