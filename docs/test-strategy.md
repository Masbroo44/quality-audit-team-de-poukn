# Stratégie de test

J'audite QuickOrder V3.1 (commit `d4606da`) avant sa mise en production. L'application tourne en local avec Docker, sur la base de démo remise à zéro avant la campagne. Je n'ai pas modifié son code.

## Périmètre

- Inscription et connexion
- Recherche et filtres
- Panier et stock
- Checkout, coupons et paiement simulé (carte, PayPal, espèces)
- Suivi et annulation des commandes
- API REST, testée dans Swagger avec la clé `X-API-Key`

## Hors périmètre

- Performance et charge, l'application tourne en local avec le serveur de développement Flask
- Sécurité poussée, je me limite à la connexion, aux droits d'accès et à la clé API
- Autres navigateurs que Chromium, et le mobile
- Accessibilité
- Administration, profil, avis et favoris, jugés moins critiques
- Tests utilisateurs

## Parcours critiques

1. Paiement, parce que l'argent du client est en jeu.
2. Passage de commande, où s'appliquent les règles (restaurant ouvert, minimum, adresse).
3. Coupons, qui changent le montant payé.
4. Panier et stock, sinon le restaurant reçoit des commandes qu'il ne peut pas servir.
5. Connexion, qui protège les commandes de chaque client.

L'API est testée en plus sur ces parcours, car elle permet de commander sans passer par le site.

## Risques

- Un montant payé faux (coupon, espèces, double paiement)
- Une commande payée mais impossible à livrer
- Un stock qui n'est pas respecté
- Une API qui n'applique pas les mêmes règles que le site
- L'accès aux commandes d'un autre client

## Types de tests

- Tests fonctionnels de bout en bout dans le navigateur, avec des cas nominaux, limites, d'erreur et de règles métier
- Tests API dans Swagger (codes HTTP, réponses JSON, clé API)
- Quelques tests de sécurité simples (mauvais mot de passe, clé absente, redirection après connexion)
- Un smoke test après l'installation (accueil, `/api/health`, Swagger, connexion)

J'ai utilisé DevTools pour suivre les requêtes envoyées, et Playwright pour rejouer les parcours et prendre les captures.

## Priorisation risque × impact

Le détail est dans [risk-matrix.md](risk-matrix.md). Le paiement et la commande ont le risque et l'impact les plus forts, ils passent en premier. 14 cas sur 24 portent sur le paiement, la commande, les coupons et le panier.
