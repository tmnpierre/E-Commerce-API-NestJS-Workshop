# Api Nest : Boutique en ligne

# Objectifs

Vous devez créer une API simple avec Nest qui permettra à des utilisateurs de votre site web d'enregitrer les articles qu'ils souhaitent vendre. Cela implique que les utilisateurs doivent pouvoir ajouter des articles, ainsi que retirer leurs articles de votre site. Ils doivent aussi pouvoir consulter les articles mis en ligne par d'autres utilisateurs.

<details open><summary><h2>Prise en main</h2></summary>

1. Créer un projet Nest. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/01-cr%C3%A9er-un-projet-nest))
2. Inspecter le dossier `src` du projet Nest pour trouver : ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/02-inspecter-src))
   1. Un controlleur (Controller)
   2. Un service
3. Créer une nouvelle route nommée "direBonjour" dans ce controller. ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/03-cr%C3%A9er-une-route))
4. Créer une méthode nommée "logiqueDeDireBonjour" dans ce service. Cette méthode doit renvoyer "Bonjour". ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/04-cr%C3%A9er-une-m%C3%A9thode-dans-un-service))
5. Retourner le résultat de "logiqueDeDireBonjour" par la route "direBonjour". ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/05-retourner-le-resultat))
6. Tester votre route avec Postman.
   1. L'URL par défaut de API est la suivante : `http://localhost:3000/` ([s'y rendre](http://localhost:3000/))
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

33. Installer `Swagger` en tant que dépendance du projet.
34. Configurer `Swagger` pour être utilisé par Nest.
35. Documenter le controller `Users` pour être référencé séparément dans la documentation `Swagger`.
36. Documenter les champs du DTO de création d'utilisateur en utilisant le décorateur `Swagger` approprié.

</details>