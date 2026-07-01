# Site d'évaluation en ligne — OLÉICULTURE (CRESI AgroecologIA)

10 évaluateurs · 5 questions chacun · **3 systèmes comparés en aveugle** (slots A / B / C) :
openai sans RAG · mistral (small) avec RAG · mistral (small) sans RAG.
Nuggets = grilles candidates (méthode nuggets). Ordre A/B/C tiré au sort et contrebalancé
(graine 20260629) ; la correspondance slot ↔ système est **confidentielle** (`cle_devoilement.csv`).

> Version 1 (gemini indisponible le 2026-06-29). À mettre à jour si les nuggets sont
> ré-atomisés avec gemini : régénérer `content.js` (les réponses A/B/C, elles, ne changent pas).

## Contenu du dossier (= racine du dépôt GitHub)
- `index.html` — l'application (accueil → profil → menu des questions → envoi)
- `config.js` — **seul fichier à éditer** : coller l'URL d'envoi (ENDPOINT)
- `content.js` — 5 questions, nuggets/question, réponses des 3 systèmes (généré)
- `plan.js` — qui voit quelles questions, ordre, et permutation A/B/C des systèmes (généré)
- `apps_script_Code.gs` — collecteur à coller dans un Google Sheet
- `cle_devoilement.csv` — **CONFIDENTIEL** : slot A/B/C ↔ système réel (ne pas publier… mais sans danger : ce n'est pas dans le site)
- `QR_evaluateurs.html` — planche de QR codes (à générer une fois l'URL connue)

## Étape A — collecteur Google Sheet (Apps Script)
1. Crée/ouvre un Google Sheet (compte naudin@cirad.fr) et copie son ID (dans l'URL, entre `/d/` et `/edit`).
2. Menu **Extensions → Apps Script**. Colle tout `apps_script_Code.gs`. Mets l'ID dans `var SHEET_ID = "..."` (ou laisse vide si le script est lié au Sheet). Enregistre.
3. **Déployer → Nouveau déploiement → Application web** : exécuter en tant que **Moi**, accès **Tout le monde**. Déploie, autorise, copie l'**URL /exec**.
4. Colle cette URL dans `config.js` → `ENDPOINT`. (Le script crée 3 onglets : `reponses`, `nuggets`, `ajouts`.)

## Étape B — publier le site (GitHub Pages, via GitHub Desktop)
1. Dans **GitHub Desktop** : *File → Add local repository* → choisir ce dossier `site_oleiculture/`
   (ou *Create repository* ici). Publier le dépôt (ex. `eval-oleiculture`).
   ⚠️ `index.html` est à la **racine** du dépôt (requis pour Pages).
2. Sur github.com : repo → **Settings → Pages** → Source : branche `main`, dossier `/ (root)` → Save.
3. URL publiée : `https://<compte>.github.io/eval-oleiculture/`.
4. (Optionnel) ne pas committer `cle_devoilement.csv` si tu préfères le garder hors dépôt — il n'est de toute façon pas chargé par le site.

## Étape C — liens évaluateurs
- Accueil : `https://.../eval-oleiculture/`
- Lien direct évaluateur N : `https://.../eval-oleiculture/?ev=03`
- Génère la planche QR dans `QR_evaluateurs.html` une fois l'URL connue.

## Étape D — test
Ouvre `?ev=01`, remplis une question, **Envoyer** → vérifie l'apparition de lignes dans
les onglets `reponses` / `nuggets` / `ajouts`. Sans ENDPOINT, le bouton Envoyer affiche
l'aperçu JSON (utile pour tester hors-ligne).
