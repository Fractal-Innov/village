# village

Le village 3D de Fractal Innov, publié en démonstrateur sur
https://www.fractal-innov.fr/village/

C'était la page d'accueil du site jusqu'au 25/09/2026. La racine sert
désormais une page de présentation classique ; le village garde sa vie
propre comme démonstrateur, au même titre que `/stand/` ou `/rayon-x/`.

## Ce que contient ce dépôt

Une **build Needle Engine, telle quelle**. Rien ne se compile ici : le
workflow `.github/workflows/publier.yml` prend le dossier et le publie sur
GitHub Pages. La source vit dans
`Needle5/Needle/fractal-innov/` (projet Unity + Vite).

| Fichier | Rôle |
| --- | --- |
| `index.html` | la page du village (68 Ko, tout le balisage des douze arrêts) |
| `assets/` | la build Vite : bundles, `.glb`, wasm, polices, pictogrammes hachés (13 Mo) |
| `needle-app.js`, `needle.buildinfo.json` | l'amorce Needle et l'inventaire de la build |
| `include/pictos/` | les pictogrammes chargés **en relatif** (`./include/pictos/…`) par le bundle |
| `.nojekyll` | sans lui, Pages ignore les dossiers qui commencent par un souligné |

## ⚠️ Ce qui casse si on s'y trompe

- **`include/pictos/` doit rester ici.** Le bundle le demande en `./include/pictos/…`,
  donc relativement à l'adresse de la page : depuis `/village/`, il cherche
  `/village/include/pictos/`. C'est la seule raison pour laquelle ce dossier
  est dupliqué entre ce dépôt et le dépôt racine.
- **Les autres ressources partagées restent à la racine du site**, et le
  village les demande en chemin absolu : `/contenu.json`, `/include/poster.webp`,
  `/include/polices/`, `/icones/`, `/site.webmanifest`. Elles vivent dans
  `Fractal-Innov.github.io` et ne doivent pas être recopiées ici.
- **Les liens de navigation du village pointent vers la racine du site**
  (`/produits/`, `/cas-d-usage/`, `/niveaux-et-modules/`, `/pilote-15-jours/`,
  `/methode-et-contact/`, `/webxr-dans-le-navigateur/`, `/rayon-x/`). Ces pages
  sont servies par `Fractal-Innov.github.io` : les supprimer là-bas casse la
  navigation ici, sans que rien ne rougisse.
- **Pas de `CNAME` dans ce dépôt.** Le domaine est porté par le dépôt
  d'organisation `Fractal-Innov.github.io` ; un `CNAME` ici détournerait
  `www.fractal-innov.fr` vers ce seul dépôt.

## Republier

Pousser sur `main` suffit. Pour republier sans commit : onglet Actions,
workflow « Publier sur GitHub Pages », `Run workflow`.
