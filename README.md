# Api Nest : Boutique en ligne

# Objectifs

![](./img/you-are-not-prepared.png)

Votre mission si vous l'acceptez est de créer une API simple de petites annonces avec Nest qui permettra à des utilisateurs de votre site web d'enregitrer les articles qu'ils souhaitent vendre. Cela implique que les utilisateurs doivent pouvoir ajouter des articles, ainsi que retirer leurs articles de votre site. Ils doivent aussi pouvoir consulter les articles mis en ligne par d'autres utilisateurs.
 
<details open><summary><h2>Prise en main</h2></summary>

- [x] 1. Créer un projet Nest.
- [x] 2. Inspecter le dossier `src` du projet Nest pour trouver :
   - Un controlleur (Controller)
   - Un service
- [x] 3. Créer une nouvelle route nommée "sayGoodbye" dans ce controller.
- [x] 4. Créer une méthode nommée "logicToSayGoodbye" dans ce service. Cette méthode doit renvoyer "Goodbye".
- [x] 5. Retourner le résultat de "logicToSayGoodbye" par la route "sayGoodbye".
- [x] 6. Tester votre route avec [httpie](https://httpie.io/cli) ou "Postman".
   - L'URL par défaut de l'API est la suivante : `http://localhost:3000/` ([s'y rendre](http://localhost:3000/))
- [ ] 7. Créer un nouveau controller appellé "Product".
- [ ] 8. Créer un nouveau service pour ce nouveau controller nommé "Product".
- [ ] 9. Créer une nouvelle route dans le controller `Product` qui utilise le service `Product` et renvoie un tableau de nom d'article.
- [ ] 10. Créer un nouveau module nommé `Product`.
- [ ] 11. Déplacer le controller, le service et le module `Product` dans un nouveau dossier nommé `Product`.
- [ ] 12. Lier le controller `Product` et le service `Product` dans le module `Product`.
- [ ] 13. Importer le module `Product` dans le module `App`.
- [ ] 14. Tester la route du controller `Product` avec Postman.
</details>
<details open><summary><h2>Persistance de données</h2></summary>

### ORM : Prisma

- [ ] 15. Installer `prisma` en tant que dépendance de développement du projet Nest.
- [ ] 16. Installer le client prisma (paquet `@prisma/client`) en tant que dépendance du projet.
- [ ] 17. Initialiser `prisma` dans le projet Nest.
- [ ] 18. Importer ce schéma dans le projet Nest.
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

- [ ] 19. Migrer le schéma vers la base de données.
- [ ] 20. Créer le service `Prisma`.
- [ ] 21. Vérifier que la structure de la base de données correspond à la définition du schéma Prisma.

</details>
<details open><summary><h2>Création des utilisateurs</h2></summary>

- [ ] 22. Créer une nouvelle ressource (~=module) nommée `Users` avec "Nest CLI" (Note: Une ressource est un ensemble de : controller, service, module. On appelle aussi cela un module) (Puis laisser les options par défaut). 
- [ ] 23. Ajouter les propriétés : `Pseudo` et `Mail` dans le DTO `create-user`.
- [ ] 24. Définir le service Prisma en tant que provider du module `Users`.
- [ ] 25. Implémenter la logique de la route `create` du controller `User` afin de créer un nouvel utilisateur dans la base de données.
- [ ] 26. Créer une route pour récupérer les informations d'un utilisateur par son UUID.
- [ ] 27. Créer une route pour modifier les informations d'un utilisateur.
- [ ] 28. Créer une route pour supprimer un utilisateur par son UUID.
- [ ] 29. Normaliser toutes les réponses du controller `Users` sous le format suivant : 
    - Un champ de message qui doit dire que l'opération à bien été exécutée nommé `message`.
    - Un champ de données qui doit contenir le résultat de l'opération nommé `data`.
- [ ] 30. Préparer la validation des données envoyées par l'utilisateur en utilisant la `Validation Pipe` et ses décorateurs.
- [ ] 31. Utiliser la `Validation Pipe` comme `Global Pipe`.
- [ ] 32. Transformer automatiquement les données envoyées par l'utilisateur dans le type attendu dans le DTO grâce à la `Validation Pipe`.

</details>
<details open>
<summary><h2>Documentation de l'API : Swagger</h2></summary>

- [ ] 33. Installer `Swagger` en tant que dépendance du projet.
- [ ] 34. Initialiser `Swagger` pour être utilisé par Nest.
- [ ] 35. Utiliser le décorateur `Swagger` approprié pour documenter les routes du controller `Users` séparément.
- [ ] 36. Documenter les champs du DTO de création d'utilisateur en utilisant le décorateur `Swagger` approprié.
- [ ] 37. Tester la documentation Swagger en se rendant à l'URL `http://localhost:3000/api` ([s'y rendre](http://localhost:3000/api))

</details>
<details open>
<summary><h2>CRUD pour les produits</h2></summary>

- [ ] 38. Créer une route et ses besoins annexes pour enregistrer de nouveaux article.
- [ ] 39. Créer une route pour récupérer un article par son UUID.
- [ ] 40. Créer une route et ses besoins annexes pour modifier les informations d'un article par son UUID.
- [ ] 41. Créer une route pour supprimer un article par son UUID.

</details>
<details open>
<summary><h2>Utilisation d'un service depuis un autre module</h2></summary>

- [ ] 42. Définir le service `Products` en tant que provider du module `Users`.
- [ ] 43. Créer une méthode dans le service `Products` pour récupérer tous les articles d'un utilisateur en fonction de l'UUID de l'utilisateur.
- [ ] 44. Créer une route dans le controller `Users` qui retourne les articles d'un utilisateur.
- [ ] 45. Faire la même chose pour supprimer les articles d'un utilisateur.

</details>

<details open>
<summary><h2>Authentification</h2></summary>

<details open>
<summary><h3>Préparation</h3></summary>

- [ ] 46. Modifier le schéma `Prisma` pour permettre l'authentification des utilisateurs.
- [ ] 47. Migrer le nouveau schéma `Prisma` pour mettre à jour la structure de la base de données.
- [ ] 48. Installer les paquets `@nestjs/passport`, `passport`, `@nestjs/passport-jwt`, `@nestjs/jwt` ainsi que le paquet `@types/passport-jwt` (en tant que devDep).
- [ ] 49. Installer les paquets `bcrypt` ainsi que `@types/bcrypt` (en tant que devDep) 

</details>

- [ ] 50. Créer un module `Auth` dédié à l'authentification des utilisateurs.
- [ ] 51. Modifier la route et ses besoins connexes pour enregister de nouveaux utilisateurs.
    - Adapter le `dto` pour enregistrer les nouveaux comptes.
    - Adapter la logique pour cette route :
    - Hasher le mot de passe avec `bcrypt` avant de l'enregistrer en base de données.
       - Enregistrer le nouvel utilisateur en base de données.
- [ ] 52. Créer une route pour la connexion des utilisateurs.
    - Créer une méthode dans le service `Users` pour récupérer un utilisateur par le nom d'utilisateur.
    - Utiliser le `Jwt Service` et le `Users Service` dans le module `Auth`.
    - Créer la logique pour authentifier un utilisateur.
       - Renvoyez uniquement un objet contenant un champ : `access_token` contenant le JWT signé avec les informations suivantes :
          - Le nom d'utilisateur de l'utilisateur.
          - L'UUID de l'utilisateur.
- [ ] 53. Implémenter la stratégie `Jwt` pour le module Auth.
- [ ] 54. Créer un `Guard` d'authentification.
- [ ] 55. Rendre l'authentication globale à l'API (faire que chaque route de l'API nécessite une authentification).
- [ ] 56. Permettre à certaines routes de ne pas nécessiter d'authentification grâce à un décorateur personnalisé.

</details>
