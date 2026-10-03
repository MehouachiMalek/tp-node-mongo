# Réponses aux questions de compréhension

## 1. Pourquoi l'application Android ne se connecte-t-elle pas directement à MongoDB ?
La base de données doit rester protégée : seule l'API y accède, après avoir validé les données et géré les erreurs. Passer par l'API évite d'exposer les identifiants de la base dans l'application, et permet à plusieurs clients (Android, Flutter, site web) de partager les mêmes données et les mêmes règles.

## 2. Différence entre req.body, req.params et req.query
- `req.body` : le corps JSON envoyé (POST, PUT). Exemple : `{ "nom": "Ben Salah" }`.
- `req.params` : les parties variables de l'URL. Exemple : `/api/patients/6ab5…` donne `req.params.id`.
- `req.query` : les filtres après le `?`. Exemple : `/api/patients?statut=Actif` donne `req.query.statut`.

## 3. Pourquoi 404 et non 400 pour un identifiant valide qui ne correspond à aucun patient ?
Le 400 signifie que la requête est incorrecte (identifiant mal formé). Ici l'identifiant est bien formé : la requête est correcte, mais la ressource demandée n'existe pas. Le code juste est donc 404 Not Found.

## 4. Que se passerait-il sans app.use(express.json()) ?
Le corps JSON ne serait pas transformé en objet JavaScript : `req.body` serait `undefined`. Les POST et PUT ne recevraient aucune donnée, et la création échouerait (par exemple 400 « Le nom est obligatoire » alors que le nom est envoyé).

## 5. Pourquoi l'émulateur doit-il utiliser 10.0.2.2 au lieu de localhost ?
Dans l'émulateur, `localhost` désigne l'émulateur lui-même, pas le PC. L'adresse spéciale 10.0.2.2 est redirigée vers le PC hôte, où tourne le serveur.

## 6. À quoi sert await ? Quelle notion de Kotlin lui correspond ?
`await` attend le résultat d'une opération longue (comme une requête MongoDB) sans bloquer le serveur, qui continue de traiter d'autres requêtes. Une fonction qui l'utilise doit être `async`. En Kotlin, cela correspond aux coroutines et aux fonctions `suspend`.

## Exercice Consultations : avec et sans populate
- Avec `.populate("patient", "nom prenom")` : le champ `patient` contient `nom`, `prenom` et `id` du patient (comme une jointure SQL).
- Sans populate : le champ `patient` contient seulement l'identifiant du patient (comme une clé étrangère).

## Pour aller plus loin : supprimer un patient qui a des consultations
Le code 409 Conflict me semble le plus juste : la requête est bien formée et la ressource existe, mais la suppression est en conflit avec l'état actuel des données (des consultations dépendent du patient).