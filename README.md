# Api Nest : Boutique en ligne

# Objectifs

![](./img/you-are-not-prepared.png)

Votre mission si vous l'acceptez est de créer une API simple de petites annonces avec Nest qui permettra à des utilisateurs de votre site web d'enregitrer les articles qu'ils souhaitent vendre. Cela implique que les utilisateurs doivent pouvoir ajouter des articles, ainsi que retirer leurs articles de votre site. Ils doivent aussi pouvoir consulter les articles mis en ligne par d'autres utilisateurs.
 
<details open><summary><h2>Prise en main</h2></summary>

- [ ] 1. Créer un projet Nest.
- [ ] 2. Inspecter le dossier `src` du projet Nest pour trouver :
   - [ ] 3. Un controlleur (Controller)
   - [ ] 4. Un service
- [ ] 5. Créer une nouvelle route nommée "sayGoodbye" dans ce controller.
- [ ] 6. Créer une méthode nommée "logicToSayGoodbye" dans ce service. Cette méthode doit renvoyer "Goodbye".
- [ ] 7. Retourner le résultat de "logicToSayGoodbye" par la route "sayGoodbye".
- [ ] 8. Tester votre route avec [httpie](https://httpie.io/cli) ou "Postman".
   - L'URL par défaut de l'API est la suivante : `http://localhost:3000/` ([s'y rendre](http://localhost:3000/))
- [ ] 11. Créer un nouveau controller appellé "Product".
- [ ] 12. Créer un nouveau service pour ce nouveau controller nommé "Product".
- [ ] 13. Créer une nouvelle route dans le controller `Product` qui utilise le service `Product` et renvoie un tableau de nom d'article.
- [ ] 14. Créer un nouveau module nommé `Product`.
- [ ] 15. Déplacer le controller, le service et le module `Product` dans un nouveau dossier nommé `Product`.
- [ ] 16. Lier le controller `Product` et le service `Product` dans le module `Product`.
- [ ] 17. Importer le module `Product` dans le module `App`.
- [ ] 18. Tester la route du controller `Product` avec Postman.
</details>
<details open><summary><h2>Persistance de données</h2></summary>

### ORM : Prisma

- [ ] 19. Installer `prisma` en tant que dépendance de développement du projet Nest.
- [ ] 20. Installer le client prisma (paquet `@prisma/client`) en tant que dépendance du projet.
- [ ] 21. Initialiser `prisma` dans le projet Nest.
- [ ] 22. Impo rter ce schéma dans le projet Nest.
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

- [ ] 23. Migrer le schéma vers la base de données.
- [ ] 24. Créer le service `Prisma`.
- [ ] 25. Vérifier que la structure de la base de données correspond à la définition du schéma Prisma.

</details>
<details open><summary><h2>Création des utilisateurs</h2></summary>

- [ ] 27. Créer une nouvelle ressource (~=module) nommée `Users` avec "Nest CLI" (Note: Une ressource est un ensemble de : controller, service, module. On appelle aussi cela un module) (Puis laisser les options par défaut). 
- [ ] 28. Ajouter les propriétés : `Pseudo` et `Mail` dans le DTO `create-user`.
- [ ] 29. Définir le service Prisma en tant que provider du module `Users`.
- [ ] 30. Implémenter la logique de la route `create` du controller `User` afin de créer un nouvel utilisateur dans la base de données.
- [ ] 31. Créer une route pour récupérer les informations d'un utilisateur par son UUID.
- [ ] 32. Créer une route pour modifier les informations d'un utilisateur.
- [ ] 33. Créer une route pour supprimenr un utilisateur par son UUID.
- [ ] 34. Normaliser toutes les réponses du controller `Users` sous le format suivant : 
    - [ ] Un champ de message qui doit dire que l'opération à bien été exécutée nommé `message`.
    - [ ] Un champ de données qui doit contenir le résultat de l'opération nommé `data`.
- [ ] 35. Préparer la validation des données envoyées par l'utilisateur en utilisant la `Validation Pipe` et ses décorateurs.
- [ ] 36. Utiliser la `Validation Pipe` comme `Global Pipe`.
- [ ] 37. Transformer automatiquement les données envoyées par l'utilisateur dans le type attendu dans le DTO grâce à la `Validation Pipe`.

</details>
<details open>
<summary><h2>Documentation de l'API : Swagger</h2></summary>

- [ ] 38. Installer `Swagger` en tant que dépendance du projet.
- [ ] 39. Initialiser `Swagger` pour être utilisé par Nest.
- [ ] 40. Utiliser le décorateur `Swagger` approprié pour documenter les routes du controller `Users` séparément.
- [ ] 41. Documenter les champs du DTO de création d'utilisateur en utilisant le décorateur `Swagger` approprié.
- [ ] 42. Tester la documentation Swagger en se rendant à l'URL `http://localhost:3000/api` ([s'y rendre](http://localhost:3000/api))

</details>
<details open>
<summary><h2>CRUD pour les produits</h2></summary>

- [ ] 43. Créer une route et ses besoins annexes pour enregistrer de nouveaux article.
- [ ] 44. Créer une route pour récupérer un article par son UUID.
- [ ] 45. Créer une route et ses besoins annexes pour modifier les informations d'un article par son UUID.
- [ ] 46. Créer une route pour supprimer un article par son UUID.

</details>
<details open>
<summary><h2>Utilisation d'un service depuis un autre module</h2></summary>

- [ ] 47. Définir le service `Products` en tant que provider du module `Users`.
- [ ] 48. Créer une méthode dans le service `Products` pour récupérer tous les articles d'un utilisateur en fonction de l'UUID de l'utilisateur.
- [ ] 49. Créer une route dans le controller `Users` qui retourne les articles d'un utilisateur.
- [ ] 50. Faire la même chose pour supprimer les articles d'un utilisateur.

</details>

<details open>
<summary><h2>Authentification</h2></summary>

<details open>
<summary><h3>Préparation</h3></summary>

- [ ] 51. Modifier le schéma `Prisma` pour permettre l'authentification des utilisateurs.
- [ ] 52. Migrer le nouveau schéma `Prisma` pour mettre à jour la structure de la base de données.
- [ ] 53. Installer les paquets `@nestjs/passport`, `passport`, `@nestjs/passport-jwt`, `@nestjs/jwt` ainsi que le paquet `@types/passport-jwt` (en tant que devDep).
- [ ] 54. Installer les paquets `bcrypt` ainsi que `@types/bcrypt` (en tant que devDep) 

</details>

- [ ] 55. Créer un module `Auth` dédié à l'authentification des utilisateurs.
- [ ] 56. Modifier la route et ses besoins connexes pour enregister de nouveaux utilisateurs.
    - [ ] 57. Adapter le `dto` pour enregistrer les nouveaux comptes.
    - [ ] 58. Adapter la logique pour cette route :
       - [ ] 59. Hasher le mot de passe avec `bcrypt` avant de l'enregistrer en base de données.
       - [ ] 60. Enregistrer le nouvel utilisateur en base de données.
- [ ] 61. Créer une route pour la connexion des utilisateurs.
    - [ ] 62. Créer une méthode dans le service `Users` pour récupérer un utilisateur par le nom d'utilisateur.
    - [ ] 63. Utiliser le `Jwt Service` et le `Users Service` dans le module `Auth`.
    - [ ] 64. Créer la logique pour authentifier un utilisateur.
       - Renvoyez uniquement un objet contenant un champ : `access_token` contenant le JWT signé avec les informations suivantes :
          - Le nom d'utilisateur de l'utilisateur.
          - L'UUID de l'utilisateur.
- [ ] 65. Implémenter la stratégie `Jwt` pour le module Auth.
- [ ] 66. Créer un `Guard` d'authentification.
- [ ] 67. Rendre l'authentication globale à l'API (faire que chaque route de l'API nécessite une authentification).
- [ ] 68. Permettre à certaines routes de ne pas nécessiter d'authentification grâce à un décorateur personnalisé.

</details>
