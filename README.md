# Sillage

Interface de chat IA — une page unique (`index.html`), sans dépendances à installer.

## ⚠️ Point important avant de déployer

Le fichier a été créé dans l'environnement Claude.ai, où les appels à
`https://api.anthropic.com/v1/messages` passent par un proxy interne qui gère
l'authentification automatiquement — c'est pour ça que ça fonctionnait sans
clé API visible.

**Une fois hébergé sur GitHub Pages (ou n'importe où en dehors de Claude.ai),
ces appels ne fonctionneront plus tels quels**, car il n'y a plus de clé API
ni de proxy. Il faut choisir une des options ci-dessous.

### Option A — Ajouter ta propre clé API (rapide, mais à usage perso uniquement)
Dans `index.html`, remplace l'appel fetch par :
```js
headers: {
  "Content-Type": "application/json",
  "x-api-key": "TA_CLE_API",
  "anthropic-version": "2023-06-01"
}
```
⚠️ Cette clé sera visible dans le code source par n'importe qui ouvrant la
page. Ne fais ça que pour un usage strictement personnel/local, jamais sur un
site public.

### Option B — Passer par un petit serveur relais (recommandé pour un vrai site)
Crée une fonction serverless (Vercel, Netlify, Cloudflare Workers...) qui reçoit
les messages du front, appelle l'API Anthropic avec ta clé stockée côté
serveur (variable d'environnement), et renvoie la réponse. Le front
(`index.html`) appelle alors ton propre endpoint au lieu d'appeler directement
`api.anthropic.com`.

## Déployer sur GitHub Pages

```bash
git init
git add .
git commit -m "Premier commit : Sillage"
git branch -M main
git remote add origin https://github.com/TON_PSEUDO/sillage.git
git push -u origin main
```

Puis dans le dépôt GitHub : **Settings → Pages → Source : branche `main`,
dossier `/ (root)`**. Le site sera en ligne à l'adresse
`https://TON_PSEUDO.github.io/sillage/` après quelques minutes.

## Structure

```
sillage/
├── index.html   ← page complète (HTML + CSS + JS)
└── README.md
```
