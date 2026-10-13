# Sophie Bluel — Portfolio d'architecte d'intérieur

Site vitrine de Sophie Bluel, une architecte d'intérieur fictive, rendu dynamique en JavaScript : la galerie de projets se charge depuis une API, se filtre par catégorie, et un espace d'administration permet d'ajouter ou de supprimer des projets.

Projet de la formation Développeuse web d'OpenClassrooms. Le back-end était fourni ; j'ai développé la partie dynamique du front-end.

## Fonctionnalités

- **Galerie dynamique** : les projets sont récupérés depuis l'API et affichés en JavaScript.
- **Filtres** : un bouton par catégorie, créé automatiquement à partir des catégories de l'API, plus un bouton « Tous ».
- **Connexion** : page de connexion de l'administratrice, avec message en cas d'identifiants incorrects.
- **Mode édition** : une fois connectée, l'administratrice ouvre une modale pour gérer ses projets.
- **Suppression** : chaque projet de la modale se supprime d'un clic.
- **Ajout** : formulaire avec envoi d'image, aperçu avant validation, contrôle du format (JPG ou PNG) et du poids (4 Mo maximum).
- **Mise à jour sans rechargement** : la galerie et la modale se rafraîchissent après chaque ajout ou suppression.

## Technologies

| Rôle | Outil |
|---|---|
| Front-end | HTML5, CSS3, JavaScript sans framework |
| Appels à l'API | `fetch` (GET, POST, DELETE), `FormData` pour l'envoi d'image |
| Authentification | Jeton JWT conservé dans le `localStorage` |
| Back-end fourni | Node.js, Express, Sequelize, SQLite |
| Documentation de l'API | Swagger |

## Installation

Prérequis : Node.js. Le site a besoin de l'API pour fonctionner, il faut donc lancer les deux parties.

```bash
git clone https://github.com/Oudin-Deborah/oc_project2.git
cd oc_project2
```

**1. Lancer l'API**

```bash
cd Backend
npm install
npm start
```

L'API écoute sur <http://localhost:5678>. Laisser ce terminal ouvert. La documentation Swagger est disponible sur <http://localhost:5678/api-docs/>.

**2. Lancer le site**

Ouvrir `FrontEnd/index.html` avec l'extension Live Server de VS Code.

**Compte de test** (fourni avec le projet) :

| E-mail | Mot de passe |
|---|---|
| `sophie.bluel@test.tld` | `S0phie` |

## Structure du projet

```
├── Backend/                 API fournie (Express, Sequelize, SQLite)
└── FrontEnd/
    ├── assets/              Feuilles de style, icônes et images
    ├── index.html           Page publique : présentation, galerie, contact
    ├── Login.html           Page de connexion
    ├── homepageEdit.html    Page d'accueil en mode édition
    ├── scriptAPI.JS         Galerie et filtres de la page publique
    ├── loginAPI.js          Connexion et stockage du jeton
    ├── editMode.js          Galerie du mode édition et déconnexion
    └── modalApp.js          Modale : suppression, ajout, aperçu de l'image
```

## Choix techniques

- **Filtres générés depuis l'API** : ajouter une catégorie côté serveur fait apparaître son bouton sans toucher au code.
- **Un seul écouteur pour tous les filtres** : le clic est capté sur le conteneur, puis identifié grâce à l'attribut `data-id` du bouton.
- **Modale à deux vues** : la suppression et l'ajout partagent la même fenêtre, on passe de l'une à l'autre en affichant ou masquant un bloc.
- **Gestion du focus** : à l'ouverture, le focus va sur le bouton de fermeture ; à la fermeture, il revient sur l'élément qui avait ouvert la modale.
- **Contrôles avant envoi** : le type et le poids de l'image sont vérifiés dans le navigateur, ce qui évite un aller-retour inutile avec le serveur.

## Pistes d'amélioration

- Regrouper le code commun aux pages (appels à l'API, affichage de la galerie) dans un seul fichier.
- Ne plus écrire l'adresse de l'API en dur, pour pouvoir mettre le site en ligne.
- Remplacer les fenêtres d'alerte par des messages affichés dans le formulaire.
- Insérer les textes venus de l'API avec `textContent` plutôt qu'`innerHTML`, plus sûr.
- Vérifier la présence du jeton avant d'afficher la page d'édition.

## Crédits

- Maquette, contenus et back-end : OpenClassrooms.
- Développement front-end : Déborah Oudin — [Portfolio](https://oudin-deborah.github.io/Portfolio/) · [LinkedIn](https://www.linkedin.com/in/oudin-deborah/) · [GitHub](https://github.com/Oudin-Deborah)
