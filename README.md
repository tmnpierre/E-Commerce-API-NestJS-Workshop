# Api Nest : Boutique en ligne

# Objectifs

Vous devez créer une API simple avec Nest qui permettra à des utilisateurs de votre site web d'enregitrer les articles qu'ils souhaitent vendre. Cela implique que les utilisateurs doivent pouvoir ajouter des articles, ainsi que retirer leurs articles de votre site. Ils doivent aussi pouvoir consulter les articles mis en ligne par d'autres utilisateurs.

<details open><summary><h2>Prise en main</h2></summary>

1. Créer un projet Nest. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/01-cr%C3%A9er-un-projet-nest))
2. Inspecter le dossier `src` du projet Nest pour trouver : ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/02-inspecter-src))
   1. Un controlleur (Controller)
   2. Un service
3. Créer une nouvelle route nommée "sayGoodbye" dans ce controller. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/03-cr%C3%A9er-une-route))
4. Créer une méthode nommée "logicToSayGoodbye" dans ce service. Cette méthode doit renvoyer "Goodbye". ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/04-cr%C3%A9er-une-m%C3%A9thode-dans-un-service))
5. Retourner le résultat de "logicToSayGoodbye" par la route "sayGoodbye". ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/05-retourner-le-resultat))
6. Tester votre route avec Postman.
   1. L'URL par défaut de l'API est la suivante : `http://localhost:3000/` ([s'y rendre](http://localhost:3000/))
7. Créer un nouveau controller appellé "Product". ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/07-cr%C3%A9er-un-controller))
8. Créer un nouveau service pour ce nouveau controller nommé "Product". ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/08-cr%C3%A9er-un-service))
9. Créer une nouvelle route dans le controlleur `Product` qui utilise le service `Product` et renvoie un tableau de nom d'article. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/09-cr%C3%A9er-une-route))
10. Créer un nouveau module nommé `Product`. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/10-cr%C3%A9er-un-module-product))
11. Tranférer le controlleur, le service et le module `Product` dans un nouveau dossier nommé `Product`. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/11-transf%C3%A9rer-dans-un-dossier))
12. Lier le controlleur `Product` et le service `Product` dans le module `Product`. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/12-lier-controller-et-service-au-module))
13. Importer le module `Product` dans le module `App`. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/13-importer-module-product-dans-module-app))
14. Tester la route de votre controlleur `Product` avec Postman.
</details>
<details open><summary><h2>Persistance de données</h2></summary>

### ORM : Prisma

15. Installer `prisma` en tant que dépendance de développement du projet Nest. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/15-installer-prisma))
16. Installer le client prisma (paquet `@prisma/client`) en tant que dépendance du projet. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/16-installer-le-client-prisma))
17. Initialiser `prisma` dans le projet Nest. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/17-initialiser-prisma))
18. Importer ce schéma dans le projet Nest. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/18-importer-le-sch%C3%A9ma))
<details>  
<summary>Schéma</summary>

```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DB_URL")
}

model Products {
  UUID        String @id(map: "products_uuid") @unique() @default(uuid()) @db.VarChar(36) //UUIDv4
  Name        String @db.VarChar(50)
  Price       Int
  Description String @db.Text()
  authorUUID  String @db.VarChar(36) // Ref to UUIDv4
  Author      Users  @relation(map: "product_author", fields: [authorUUID], references: [UUID])
}

model Users {
  UUID     String     @id(map: "users_uuid") @unique() @default(uuid()) @db.VarChar(36) //UUIDv4
  Pseudo   String     @unique() @db.VarChar(50)
  Mail     String     @unique() @db.VarChar(75)
  Products Products[]
}
```

</details>

19. Migrer le schéma vers la base de données. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/19-migrer-le-sch%C3%A9ma))
20. Créer le service `Prisma`. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/20-cr%C3%A9er-le-service-prisma)) 
21. Vérifier que la structure de la base de données correspond à la définition du schéma Prisma.

</details>
<details open><summary><h2>Création des utilisateurs</h2></summary>

22. Créer une nouvelle ressource (~=module) nommée `Users` avec "Nest CLI" (Note: Une ressource est un ensemble de : controller, service, module. On appelle aussi cela un module). ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/22-cr%C3%A9er-ressource-users)) 
23. Ajouter les propriétés : `Pseudo` et `Mail` dans le DTO `create-user`. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/23-ajouter-les-propri%C3%A9t%C3%A9s-au-dto)) 
24. Définir le service Prisma en tant que provider du module `Users`. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/24-utiliser-le-service-prisma-comme-provider)) 
25. Implémenter la logique de la route `create` du controller `User` afin de créer un nouvel utilisateur dans la base de données. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/25-impl%C3%A9menter-la-logique-de-la-route-create)) 
26. Créer une route pour récupérer les informations d'un utilisateur par son UUID. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/26-cr%C3%A9er-une-route-pour-r%C3%A9cup%C3%A9rer))
27. Créer une route pour modifier les informations d'un utilisateur. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/27-cr%C3%A9er-une-route-pour-modifier))
28. Créer une route pour supprimenr un utilisateur par son UUID. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/28-cr%C3%A9er-une-route-pour-supprimenr))
29. Normaliser toutes les réponses du controller `Users` sous le format suivant : 
    1. Un champ de message qui doit dire que l'opération à bien été exécutée nommé `message`.
    2. Un champ de données qui doit contenir le résultat de l'opération nommé `data`. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/29-normaliser-les-r%C3%A9ponses))
30. Préparer la validation des données envoyées par l'utilisateur en utilisant la `Validation Pipe` et ses décorateurs. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/30-valider-les-entr%C3%A9es-utilisateurs))
31. Utiliser la `Validation Pipe` comme `Global Pipe`. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/31-utiliser-la-validation-pipe))
32. Transformer automatiquement les données envoyées par l'utilisateur dans le type attendu dans le DTO grâce à la `Validation Pipe`. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/32-tranformer-automatiquement-les-donn%C3%A9es))

</details>
<details open>
<summary><h2>Documentation de l'API : Swagger</h2></summary>

33. Installer `Swagger` en tant que dépendance du projet.([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/33-installer-swagger))
34. Configurer `Swagger` pour être utilisé par Nest. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/34-configurer-swagger))
35. Utiliser le décorateur `Swagger` approprié pour documenter les routes du controller `Users` séparément. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/35-documenter-le-controller-users))
36. Documenter les champs du DTO de création d'utilisateur en utilisant le décorateur `Swagger` approprié. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/36-documenter-les-champs-d'un-dto))
37. Tester la documentation Swagger en se rendant à l'URL `http://localhost:3000/api` ([s'y rendre](http://localhost:3000/api))

</details>
<details open>
<summary><h2>CRUD pour les produits</h2></summary>

38. Créer une route et ses besoins annexes pour enregistrer de nouveaux article. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/38-cr%C3%A9er-une-route-pour-enregistrer-de-nouveaux-articles))
39. Créer une route pour récupérer un article par son UUID. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/39-cr%C3%A9er-une-route-pour-r%C3%A9cup%C3%A9rer-un-produit))
40. Créer une route et ses besoins annexes pour modifier les informations d'un article par son UUID. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/40-cr%C3%A9er-une-route-pour-modifier-un-produit))
41. Créer une route pour supprimer un article par son UUID. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/41-cr%C3%A9er-une-route-pour-supprimer-un-article))

</details>
<details open>
<summary><h2>Utilisation d'un service depuis un autre module</h2></summary>

42. Définir le service `Products` en tant que provider du module `Users`. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/42-d%C3%A9finir-le-service-product-en-tant-que-provider-du-module-users))
43. Créer une méthode dans le service `Products` pour récupérer tous les articles d'un utilisateur en fonction de l'UUID de l'utilisateur. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/43-cr%C3%A9er-une-m%C3%A9thode-dans-le-service-pour-r%C3%A9cup%C3%A9rer-les-articles))
44. Créer une route dans le controller `Users` qui retourne les articles d'un utilisateur. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/44-cr%C3%A9er-une-route-pour-r%C3%A9cup%C3%A9rer-les-articles))
45. Faire la même chose pour supprimer les articles d'un utilisateur. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/45-on-prend-les-m%C3%AAmes-et-on-recommence))

</details>

<details open>
<summary><h2>Authentification</h2></summary>

<details open>
<summary><h3>Préparation</h3></summary>

46. Modifier le schéma pour permettre l'authentification des utilisateurs
47. Migrer le nouveau schéma `Prisma` pour mettre à jour la structure de la base de données

</details>

</details>