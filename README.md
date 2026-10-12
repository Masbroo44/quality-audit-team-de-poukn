# Audit qualité de QuickOrder

Samuel DE POUKN, TP individuel du cours Tests et qualité des solutions numériques. J'ai audité QuickOrder V3.1 avant sa mise en production.

J'ai écrit et exécuté 24 cas de test (11 Pass, 12 Fail, 1 Blocked) et documenté 11 bugs, dont 2 critiques sur le paiement. Ma recommandation est No-Go.

- [Stratégie de test](docs/test-strategy.md)
- [Matrice risque × impact](docs/risk-matrix.md)
- [Cas de test](docs/test-cases.xlsx) (fichier Excel à télécharger, GitHub ne l'affiche pas)
- [Rapport d'exécution](docs/execution-report.md)
- [Bug reports](docs/bug-reports/)
- [Plan d'amélioration](docs/improvement-plan.md)

La partie tests utilisateurs ne fait pas partie de ce rendu.

J'ai testé le commit `d4606da` de [Masbroo44/quickorder-qa-project](https://github.com/Masbroo44/quickorder-qa-project), sans modifier le code.
