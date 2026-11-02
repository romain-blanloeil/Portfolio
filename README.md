# RCSSBG – Journées à domicile (École de rugby 2026-2027)

Page web unique pour répartir les tâches des journées à domicile :
référent APERO (ouverture / fermeture du bar, collation des coachs), bar (3), goûter (3 préparation + 2 service).

## Mise en ligne

1. **Google Sheet** (idéalement sur un compte Google du club) : trois onglets.
   - `Matchs` : en-têtes `Catégorie` | `Titre` | `Référent APERO`. Une ligne par rencontre, par exemple
     `M8` | `Plateau - le 14 novembre 2026 - 9h à 12h` | `Sophie`.
     Catégories : M6, M8, M10, M12, M14 (`M08` ou `U8` sont aussi reconnus).
   - `APERO` : en-tête `Prénom`, puis un membre par ligne.
   - `Inscriptions` : en-têtes `Match` | `Créneau` | `Prénom` | `Date` (remplissage automatique).
2. **Liste déroulante Référent APERO** : sélectionner la colonne C de `Matchs`, puis
   *Données > Validation des données > Liste déroulante (à partir d'une plage)* : `APERO!A2:A`.
   Cocher « Refuser la saisie » pour bloquer les fautes de frappe.
3. **Apps Script** : dans le Sheet, *Extensions > Apps Script*, coller `Code.gs`, puis
   *Déployer > Nouveau déploiement > Application Web* : exécuter **en tant que moi**, accès **tout le monde**.
   Copier l'URL obtenue.
4. **index.html** : coller cette URL dans `CONFIG.API_URL` et choisir un `ADMIN_CODE` personnel.
5. **Vercel** : pousser `index.html`, `style.css` et `logo.png` dans un dépôt GitHub (privé conseillé : il contient `ADMIN_CODE`), puis sur Vercel
   *Add New > Project > Import* (aucun framework). Chaque `git push` met le site à jour.
   Adresse : `rcssbg-benevolat.vercel.app`.

## Liens à partager

- Une catégorie : `rcssbg-benevolat.vercel.app/#m8` (idem `#m6`, `#m10`, `#m12`, `#m14`, `#seniors`).
  Les anciens liens `?cat=m8` fonctionnent aussi.
- Admin : `rcssbg-benevolat.vercel.app/?admin=TON_CODE` (à garder en favori, ne pas partager).
  Aucun bouton ne mène à la vue admin : on y accède uniquement par cette adresse.
  En mode démo (sans `API_URL`), `…/#admin` suffit.

## Au quotidien

- **Ajouter une rencontre** : une ligne dans `Matchs`. Format du titre :
  `Type - le JJ mois AAAA - HHh à HHh` (Atelier, Plateau ou Tournoi).
  Ne pas modifier un titre après ouverture des inscriptions : elles y sont rattachées.
- **Événement du club** (ex. tournoi annuel) : catégorie `CLUB`, par exemple
  `CLUB` | `Tournoi du club - le 5 juin 2027`. Il apparaît dans toutes les catégories,
  sans créneaux, avec un message de rappel (inscriptions auprès de l'APERO, texte dans `CONFIG.MSG_CLUB`).
- **Match seniors** : catégorie `SENIORS`, par exemple `SENIORS` | `Match seniors - le 15 novembre 2026`.
  Liste ouverte et sans limite pour les enfants (accompagnement des joueurs, ramasseurs de balles).
  Lien à partager : `rcssbg-benevolat.vercel.app/#seniors`.
- **Désigner le membre APERO référent** (bar + collation coachs) : choisir le prénom dans la colonne C. Vide = « À désigner (APERO) ».
  Personne ne peut s'inscrire sur ce créneau depuis la page.
- **Corriger une inscription** : modifier ou supprimer la ligne dans `Inscriptions`.

## Sans l'URL de l'API

La page fonctionne en mode démo (vraies dates, inscriptions enregistrées sur l'appareil) pour tester.

## Démo publiée (claude.ai)

`python3 build-artifact.py` génère `artifact/benevolat-rcssbg.html` (même code, avec `style.css` et `logo.png` intégrés)
pour republier la démo partageable.

## Nouvelle saison

Changer `SAISON_DEBUT` dans `CONFIG` (début septembre), vider l'onglet `Inscriptions`, saisir les nouvelles rencontres.

## Licence

Code sous licence MIT (voir `LICENSE`) © 2026 Romain Blanloeil (whit3roro).
Le logo et le nom du RCSSBG appartiennent au club et ne sont pas couverts par cette licence.
