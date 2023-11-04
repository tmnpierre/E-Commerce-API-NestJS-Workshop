# Api Nest : Boutique en ligne

# Objectifs

Vous devez créer une API simple avec Nest qui permettra à des utilisateurs de votre site web d'enregitrer les articles qu'ils souhaitent vendre. Cela implique que les utilisateurs doivent pouvoir ajouter des articles, ainsi que retirer leurs articles de votre site. Ils doivent aussi pouvoir consulter les articles mis en ligne par d'autres utilisateurs.

## Initialisation

1. Créer un projet Nest ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/01-cr%C3%A9er-un-projet-nest))
2. Inspecter le dossier `src` de votre projet Nest pour trouver : ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/02-inspecter-src))
   1. Un controlleur (Controller)
   2. Un service
3. Créer une nouvelle route nommée "direBonjour" dans ce controller ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/03-cr%C3%A9er-une-route))
4. Créer une méthode dans nommée "logiqueDeDireBonjour" dans ce service. Cette méthode doit renvoyer "Bonjour" ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/04-cr%C3%A9er-une-m%C3%A9thode-dans-un-service))
5. Retourner le résultat de "logiqueDeDireBonjour" par la route "direBonjour" ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/05-retourner-le-resultat))
6. Tester votre route avec Postman
   1. L'URL de votre API est la suivante `http://localhost:3000/` ([s'y rendre](http://localhost:3000/))
7. Créer un nouveau controller appellé "Product" ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/07-cr%C3%A9er-un-controller))
8. Créer un nouveau service pour ce nouveau controller appellé "Product" ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/08-cr%C3%A9er-un-service))
9. Créer une nouvelle route dans le controlleur `Product` qui utilise le service `Product` et renvoie un tableau de nom d'article ([solution de l'étape](https://github.com/benjGam/E-Commerce-API-NW/tree/09-cr%C3%A9er-une-route))
10. Créer un nouveau module nommé `Product`
11. Lier le controlleur `Product` et le service `Product` dans le module `Product`