# Mettre BailFacile en ligne (Render) — pas à pas

Résultat : une adresse web (https://bailfacile-xxxx.onrender.com) où locataires et propriétaires créent leur compte. Les comptes, dossiers, pièces, baux et loyers sont conservés.

**Coût** : l'offre gratuite de Render n'a pas de disque persistant ; il faut l'offre « Starter » (environ 7 $/mois) plus le disque (environ 0,25 $ par Go et par mois). Vérifiez les tarifs actuels sur render.com/pricing.

## 1. Mettre le dossier sur GitHub
1. Créez un compte gratuit sur github.com, puis un nouveau dépôt **privé** nommé `bailfacile`.
2. Décompressez `bailfacile.zip` sur votre ordinateur.
3. Sur la page du dépôt : « Add file » > « Upload files », glissez **tout le contenu** du dossier `bailfacile` (y compris `render.yaml` et le dossier `public`), puis « Commit changes ».

## 2. Créer le service sur Render
1. Créez un compte sur render.com et reliez-le à GitHub.
2. « New » > **Blueprint**, choisissez le dépôt `bailfacile`, puis « Apply ».
3. Attendez la fin du déploiement (quelques minutes). Render affiche l'adresse du site : ouvrez-la, créez un compte.

## 3. Activer les vrais e-mails (facultatif mais recommandé)
Sans cette étape, tout fonctionne mais les alertes ne sont que listées dans l'onglet « Alertes e-mail ».
1. Créez un compte sur resend.com, ajoutez votre nom de domaine et recopiez les enregistrements DNS demandés (SPF, DKIM) chez votre registrar.
2. Créez une clé API Resend.
3. Dans Render : votre service > **Environment** > ajoutez `RESEND_API_KEY` (la clé) et `MAIL_FROM` (par exemple `BailFacile <alertes@votre-domaine.fr>`). Le service redémarre tout seul.

## 4. Nom de domaine personnalisé (facultatif)
Render > votre service > Settings > Custom Domains. Puis ajoutez la variable `APP_URL` avec votre adresse (elle sert dans les liens des e-mails).

## Sauvegardes
Toute la base est dans un seul fichier, `/data/bailfacile.db`. Faites des sauvegardes régulières (voir la page « Disks » de votre service sur Render).

## Données de démonstration (facultatif)
Dans Render > Shell du service : `node seed.js` crée un compte propriétaire d'essai et 10 annonces. À ne pas lancer sur le site définitif.
