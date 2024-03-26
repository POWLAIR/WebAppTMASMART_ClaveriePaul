# Blog de Basketball

Ce projet est un blog simple sur le basketball, construit avec PHP et JSON comme système de stockage de données.

## Fonctionnalités

- Affichage des articles de blog
- Ajout de nouveaux articles
- Édition d'articles existants
- Suppression d'articles

## Workflow GitHub Actions

```yml
name: CI
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Set up PHP
        uses: shivammathur/setup-php@v2
        with:
          php-version: '7.4'
      - name: Install dependencies
        run: composer install --no-dev --optimize-autoloader
      - name: Run PHPMD
        run: vendor/bin/phpmd src text cleancode,codesize
      - name: Run PHPCS
        run: vendor/bin/phpcs --standard=PSR12 src
```

## Structure du Projet

Le projet est structuré comme suit :

- `data/`: Contient le fichier `posts.json` avec les données des articles.
- `includes/`: Contient les fichiers d'en-tête et de navigation.
- `src/`: Contient les principaux scripts PHP du blog.
- `vendor/`: Contient les dépendances de Composer (si utilisé).

## Installation

1. Clonez le dépôt sur votre serveur local ou de production.
2. Assurez-vous que PHP est installé sur votre système.
3. Donnez les permissions nécessaires pour que le serveur Web puisse écrire dans le fichier `data/posts.json`.
4. Assurez-vous de bien indenter le bloc de code YAML du workflow GitHub Actions pour une lisibilité optimale.

5. Enregistrez les modifications apportées au fichier README.md.

6. Faites un commit de vos modifications et poussez-les sur votre dépôt GitHub.

## Utilisation

Pour visualiser le blog, ouvrez le fichier `index.php` dans votre navigateur.

Pour ajouter, éditer ou supprimer un article, naviguez vers les pages correspondantes via l'interface du blog.

## Exemples de Code

### Ajout d'un Article

Pour ajouter un article, utilisez le formulaire dans `add_post.php`. Les données du formulaire sont envoyées à `save_post.php`.

~~~php
// Extrait de fichier add_post.php
<form action="save_post.php" method="POST">
    <label for="title">Titre de l'article :</label>
    <input type="text" id="title" name="title" required>
    ...
    <button type="submit">Publier</button>
</form>
~~~

### Suppression d'un Article

La suppression se fait via un appel JavaScript qui poste l'ID de l'article à `delete_post.php`.

~~~javascript
// Extrait de fichier index.php
<a href="#" onclick="confirmDelete(<?php echo $post['id']; ?>)">Supprimer</a>

// Extrait de fichier delete_post.php
<?php
include 'functions.php';
...
deletePost($id);
...
?>
~~~

### Édition d'un Article

Pour éditer un article, utilisez le formulaire dans `edit_post.php`. Les modifications sont envoyées à `update_post.php`.

~~~php
// Extrait de fichier edit_post.php
<form action="update_post.php" method="POST">
    <input type="hidden" name="id" value="<?php echo $post['id']; ?>">
    ...
    <button type="submit">Mettre à jour</button>
</form>
~~~

## Contribution

Les contributions sont les bienvenues. Veuillez ouvrir une issue pour discuter de ce que vous souhaitez changer ou soumettre directement une pull request.
