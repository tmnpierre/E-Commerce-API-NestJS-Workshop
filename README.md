# Api Nest : Boutique en ligne

# Objectifs

Vous devez créer une API simple avec Nest qui permettra à des utilisateurs de votre site web d'enregitrer les articles qu'ils souhaitent vendre. Cela implique que les utilisateurs doivent pouvoir ajouter des articles, ainsi que retirer leurs articles de votre site. Ils doivent aussi pouvoir consulter les articles mis en ligne par d'autres utilisateurs.

## Initialisation

1. Créer un projet Nest
2. Inspecter le dossier `src` de votre projet Nest pour trouver :
   1. Un controlleur (Controller)
   2. Un service
3. Créer une route dans le controlleur que vous avez trouvé, son nom doit être "direBonjour"
4. Créer une méthode dans le service appelé "logiqueDeDireBonjour" que vous avez trouvé qui renvoie "Bonjour"
5. Retourner le résultat de la méthode que vous avez crée dans le code de la route que vous avez crée
6. Tester votre route avec Postman
   1. L'URL de votre API est la suivante `http://localhost:3000/` (<a href="http://localhost:3000/" target="_blank" rel="noopener noreferrer">s'y rendre</a>)
7. Créer un controller appellé "Product"
8. Créer un service pour ce nouveau controller appellé "Product"
9. Créer une route dans ce controlleur pour récupérer un tableau de nom de produit
10. Lier ce nouveau controlleur dans Nest
11. Tester la route pour récupérer un tableau de nom de produit