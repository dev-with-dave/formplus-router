# Form+ router

## TOPO

Au programe aujourd'hui: on met en place un router en PHP.

Le gérant d'une salle de sport est venu nous voir pour nous demander de migrer son site (pour le moment en HTML) vers PHP.
Le client est plutôt préssé et aimerait que le travail soit fait dans la journée.

Le site comporte quatres pages pour le moment mais sera certainement amené à évoluer. Notre travail ici va être d'utiliser la puissance de PHP pour découper le site de manière à ce que le code soit le plus `D`('ont) `R`(epeat) `Y`(ourself) possible. On ne va donc pas hésiter à créer plusieurs petits fichiers et à les inclure les uns dans les autres (en fonction des besoins bien entendu).

Une fois la migration vers PHP terminée et le site découpé en plusieurs fichiers, nous allons implémenter un router. Nous avons la possibilité de le coder nous même ou d'utiliser des dépendances (comme AltoRouter par exemple), tout ceci en adoptant l'approche `M`(odel) `V`(iew) `C`(ontroller).

Enfin si la deadline le permet plutôt que d'utiliser des fichiers comportant l'extension `.php` on viendra rajouter le moteur de template `twig`.

---

### Transformation HTML -> PHP

En forme? Prêt à commencer? Bon de toute façon vu que le client est préssé et qu'il veut que le travail soit terminé dans la journée... on a pas tellement le choix. 😬

Pour cette transformation HTML -> PHP on va d'abord faire un tour d'horizon des fichiers pour voir ce qui se repète dans chaque fichier.

- Est-ce que le header est utilisé partout?
- Est-ce que le footer est utilisé partout?
- Est-ce qu'un modèle particulier se répète dans le code HTML?

Autant de questions qui vont nous aiguiller vers la découpe ou non de certaines parties du fichier.

<details>
  <summary>spoiler</summary>

> Attention aux modèles qui se repètent dans le HTML, on peut utiliser PHP pour faire des boucles...

</details>

---

### Router

Maintenant que le `projet` à été bien découpé et migré vers PHP, on va implémenter un router. L'implémentation du router est libre, vous pouvez utiliser la méthode que vous voulez pour créer ce router (dépendances, conditions sur la route demandée...). Ce router sera à placer dans le fichier `index.php`.

Ce fichier deviendra par extension notre point d'entrée, c'est lui qui se chargera de recevoir toutes les requêtes et de rediriger vers la bonne page.

<details>
  <summary>spoiler si vous choisissez de l'implémenter vous même</summary>
Peut-être a-t-on vu une variable superglobale qui donne plein d'infos intéressantes à propos du serveur, de l'url, etc..? 🤷‍♂️

On pourrait ensuite utiliser des conditions...

</details>

> Vous pouvez si vous le voulez utiliser la class `Router` présente dans le dossier src. Si vous optez pour cette solution il y'aura peut être des choses en plus à faire.

<details>
  <summary>spoiler si vous voulez utiliser la class Router</summary>
La class Router étends la class AltoRouter qui est une dépendance à installer avec composer

pour initialiser composer:

```bash
$ composer init
```

La dépendance à installer est AltoRouter/AltoRouter

N'oubliez pas que le code d'AltoRouter se trouve dans le dossier vendor et qu'il faudra peut-être faire quelque chose avant de pouvoir l'utiliser...

N'oubliez pas ensuite d'importer la class `Router` pour y avoir accès dans le fichier `index.php`

</details>

### **N'oubliez pas de modifier les liens dans le header!**

---

### Controller

Le travail avance plutôt bien on dirait! Bravo! 😁

- [x] Migration HTML -> PHP
- [x] Découpage des fichiers
- [x] Mise en place du Router
- [ ] Mise en place du Controller

On dirait que se rapproche de plus en plus du modèle MVC! (les modèles en moins puisque pas forcément l'utilité pour le moment 😬)

Pour cette dernière étape on va mettre en place un (ou des ? en fonctions des besoins) controller.

Ce controller sera une class PHP qui contiendra des méthodes. Dans ces méthodes on retrouvera toute la logique en lien avec une certaine page. Si on a des données à récupérer c'est ici qu'on le fera et en dernière instruction, le controller renverra la page à afficher.

Une fois le controller créé, avant de l'utiliser on pourra mettre en place l'auto-loading pour nous simplifier la tâche.

<details>
  <summary>spoiler</summary>

On peut mettre en place l'auto-loading en rajoutant la clé autoload au fichier `composer.json`

```json
{
  {
    /*
     *
     * config ...
     *
     */

    "autoload": {
      "psr-4": {
        "App\\": "src"
      }
    }
  }
}
```

</details>

> Si l'auto-loading ne fonctionne pas, il vous manque peut-être une étape (comme actualiser le fichier autoload)

<details>
<summary>spoiler</summary>

```bash
$ composer dump-autoload
```

</details>

### **Recap du chemin de la requête**:

`index.php` -> `Router` -> `Controller` -> `view`

---

<details>
  <summary>Bonus 1</summary>
  Implémenter twig.

Plutôt que de renvoyer des pages en `.php`, on va utiliser twig pour séparer un petit mieux les choses et respecter encore plus en profondeur le principe de `S`(eparation) `O`(f) `C`(oncerns).

Pour ce bonus pas d'indications supplémentaires. Servez vous de ce qu'on a déjà vu et de la [doc de twig](https://twig.symfony.com/){:target="\_blank"}

</details>
