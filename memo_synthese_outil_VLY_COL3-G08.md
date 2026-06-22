# Mémo de synthèse — Outil VLY-COL3-G08
**ADP 2026 · CRMEF Inezgane · Volleyball ES-VLB · DNB Niveau 2**
État au 15 juin 2026

---

## 1. Objet de l'outil

Outil HTML/JS autonome (un seul fichier, fonctionne hors-ligne après chargement), à deux pages :

- **Page 1 — Diagnostic & Planification** : saisie des notes de classe, calcul automatique des profils A/B/C, axes prioritaires, planification du cycle (4 étapes).
- **Page 2 — Grille d'Évaluation** : saisie terrain par équipes, deux modèles de grille (Terrain v2 / Officielle), calcul du /20, import de listes par OCR.

---

## 2. Page 1 — Diagnostic & Planification

### Étape 1 — Diagnostic de classe
- Sélecteur de niveau scolaire (1AC/2AC/3AC) : ajuste automatiquement les barèmes max d'OBS-01/02/03 selon le tableau officiel (Op2009 p.25).
- Saisie manuelle (Prénom, OBS-01/02/03, Conceptuel /3 facultatif).
- **Import CSV terrain** : détection flexible des colonnes (NOM, NOM_PRENOM, Nom_Eleve, combinaison NOM+PRENOM, séparateurs `,`/`;`/tab, en-têtes accentués ou non), avec message de détection et repli sur la 2e colonne si rien n'est reconnu.
- **Analyser** → génère :
  - Tableau individuel modernisé (en-tête bleu marine, lignes alternées, scroll horizontal) : Rang, Prénom, OBS-01/02/03, **Conceptual** (note + appréciation Maîtrise/En cours/Insuffisant), Moy./10, **Note finale /20**, Profil global (badge circulaire), Profil détaillé, Lacune(s), Axe prioritaire, Axe associé.
  - Bilan de classe (cartes A/B/C + moyennes classe /10, /20, Conceptuel).
  - Analyse par observable, groupes de besoin, décision dominante.
  - **Page "Analyse de la classe"** (plein écran actuellement, bouton ← Retour) : tableau export-ready avec badges 32px, export PDF/CSV.
- Export CSV complet, impression.

### Étape 2 — Axes prioritaires
- **Deux référentiels d'axes disponibles**, sélectionnables :
  - **TD1 (par défaut)** — "Axes Prioritaires ADP2026", lacune dominante **N1-1** (lecture de balle crise/temps). Axe 1 = lecture de balle + déplacement (OBS1+OBS2) ; Axe 2 = rôles/communication (OBS2) ; Axe 3 = projet collectif (OBS1+OBS2).
  - **TD2** — référentiel initial, lacune dominante N1-2.
- Changer de référentiel recalcule immédiatement la pertinence, l'axe associé par élève, et rafraîchit l'analyse si déjà calculée.
- Affichage modernisé : cartes `.axe-card` avec barre de pertinence (% d'élèves concernés), badges (pertinence / observable lié / priorité), impact.
- Sélection 3-4 axes obligatoire pour débloquer l'Étape 3.

### Étapes 3 & 4 — Paramétrage et Planification
- Slider 6-10 séances, distribution automatique par séquence, planification détaillée par séance (non modifiées dans cette session).

---

## 3. Page 2 — Grille d'Évaluation

- Deux modèles : **Grille Terrain v2** (OBS-01/7, OBS-02/8, COMP/4) et **Grille Officielle** (OBS-01/6, OBS-02/8, COMP/5), Conceptuel/3 dans les deux cas.
- Gestion d'équipes (drag & drop, scores de match, victoire), barème entièrement éditable (noms de critères, max, niveaux F/M/B, descriptions).
- Import de liste par photo (OCR Tesseract.js, arabe+français, local).
- **Bouton "📊 Analyser"** (nouveau) : tableau d'analyse sous le tableau de saisie — critères/labels/max lus dynamiquement depuis le barème édité (3 critères fixes OBS-01/OBS-02/COMP, conforme au référentiel), Profil par critère (seuils 75%/50%), Profil global = pire niveau, Lacune L1, axe prioritaire, **/20 jamais recalculé**. Export PDF/CSV.

---

## 4. Points en attente / décisions à prendre

1. **Flux d'affichage de l'analyse (Page 1)** : actuellement page plein écran avec "← Retour". Une demande de passage à un affichage **en dessous du tableau de saisie** (sans changer de page, tout reste visible) a été discutée et validée en principe, mais **pas encore implémentée**.
2. **Enrichissements TD1 "à valider"** (sources Eduscol/Gréhaigne, 4 compléments proposés dans le référentiel Axes Prioritaires) : non intégrés dans les `justification`/`impact` des axes — décision pédagogique en attente.
3. **Anomalies de données signalées non résolues** :
   - Grille Équipes 3-4 (photo) : **Hicham** (OBS-02 non entouré) et **Ali** (Comportemental non entouré) — valeurs manquantes à compléter.
   - Vérifier si **Mohamed/Ali Conceptuel = 4 / 4,5** (dépasse le max /3) est une erreur de lecture.
4. **Confirmation formateur attendue** (format imposé par le référentiel Axes Prioritaires) :
   > "Axes retenus — Volleyball — ES-VLB — [date] : Axe 1 : [...] · Axe 2 : [...] · Axe 3 : [...] · Mode d'entrée : B · Enrichissements intégrés : [N intégrés · N rejetés]"

---

## 5. Fichier livrable actuel
`outil_v0_VLY_COL3-G08.html` (~184 Ko, autonome, 3 blocs `<script>`, syntaxe validée).
