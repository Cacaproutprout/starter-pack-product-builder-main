# 2 - Prompt app claude : choix des technologies, bonnes pratiques et plan de développement

> Version 1.0.0 (2026-10-27). Historique des modifications en fin de fichier.

> Remplis uniquement la section **1. MON PRODUIT**, puis envoie tout à Claude Code.
> Le reste du prompt est fixe : Claude Code choisit la stack et applique les bonnes pratiques.

---

## 1. MON PRODUIT (à remplir)

- **Nom / idée en une phrase** : [...]
- **Utilisateurs cibles** : [...]
- **Problème résolu** : [...]
- **Fonctionnalités MVP (3 à 5 max)** : [...]
- **Plus tard (v2+)** : [...]
- **Plateforme** : [web / mobile / les deux / je ne sais pas]
- **Contraintes connues** (budget, délai, outils imposés, données sensibles, API externes) : [...]
- **Mon niveau technique / temps dispo** : [...]

---

## 2. RÈGLES DE FONCTIONNEMENT

- **Source de vérité = fichiers du repo (`/docs`)**, pas la conversation. À chaque démarrage : relis `/docs`.
- Mets à jour `/docs` à **chaque décision, changement ou blocage résolu**.
- **Si tu n'es pas sûr d'une info** (version, prix, compatibilité, obligation légale) : dis-le explicitement et vérifie via recherche web avant de recommander.
- **Challenge mes hypothèses.** Si une demande est floue, hors MVP ou risquée : dis-le.
- Réponses courtes, concrètes, étape par étape. Pas de pavés théoriques.

---

## 3. PHASE 0 — QUESTIONS (avant toute proposition)

Avant de proposer une stack, pose-moi **au maximum 8 questions** (une liste numérotée, courte) sur ce qui manque :

- périmètre MVP vs v2+
- volumétrie attendue (utilisateurs, données)
- données personnelles / sensibles (RGPD)
- besoin hors-ligne, temps réel, notifications, paiement, IA
- budget d'hébergement mensuel
- compétences que je veux garder (ce que je sais maintenir)

Attends mes réponses. Ne code rien à ce stade.

---

## 4. PHASE 1 — CHOIX DES TECHNOLOGIES

Pour **chaque couche utile** (frontend, backend, base de données, auth, hébergement, CI/CD, monitoring, tests, paiement/email/stockage si besoin) :

1. Propose **2 à 3 options** réalistes.
2. Compare-les dans un tableau court selon ces critères :
   - adéquation au produit et au MVP
   - maturité et activité de la communauté
   - coût (gratuit → à l'échelle)
   - simplicité de maintenance pour une personne seule
   - sécurité et conformité RGPD (hébergement UE ?)
   - risque de verrouillage fournisseur (vendor lock-in)
   - évolutivité si le produit grandit
3. **Recommande 1 option** + justification en 2 lignes max.
4. Indique la **version stable actuelle** (vérifiée par recherche web) et signale si tu as un doute.
5. Privilégie la solution **la plus simple qui couvre le MVP** (pas de microservices, Kubernetes, etc. sans besoin prouvé).

**Livrable de la phase** : `docs/ARCHITECTURE.md` + `docs/DECISIONS.md` (une entrée par choix : date, options étudiées, choix, raison, conséquences).
Puis : **attends ma validation** avant de coder.

---

## 5. PHASE 2 — BONNES PRATIQUES À APPLIQUER DÈS LE DÉPART

Applique et configure tout ce qui suit dans le projet (adapte à la stack choisie, explique si tu écartes un point).

### 5.1 Git & Pull Requests
- Branche `main` protégée, jamais de commit direct.
- Une feature = une branche = une **Pull Request**.
- Commits au format Conventional Commits (`feat:`, `fix:`, `docs:`, `test:`, `chore:`).
- Template de PR avec checklist : tests ajoutés, docs mises à jour, pas de secret, pas de warning, impact RGPD vérifié.
- Merge uniquement si la CI est verte.
- Tags de version + `CHANGELOG.md`.

### 5.2 Tests automatisés
- **Unitaires** (logique métier) — objectif de couverture : [80 % sur le code métier].
- **Intégration** (API + base de données de test).
- **End-to-end** (parcours critiques du MVP au minimum).
- Tests écrits **en même temps** que la feature, pas après.
- Tout bug corrigé = un test de non-régression.
- Les tests tournent automatiquement sur chaque PR.

### 5.3 CI/CD
- Pipeline : lint → format → tests → audit dépendances → build → déploiement.
- Environnements : local, staging, production.
- Déploiement automatisé + **plan de rollback documenté et testé**.
- Secrets dans les variables d'environnement du CI (jamais dans le code).

### 5.4 Sécurité (référence : OWASP Top 10)
- HTTPS partout, en-têtes de sécurité (CSP, HSTS, etc.).
- Validation des entrées côté client **et** serveur.
- Protection contre injection SQL (requêtes paramétrées), XSS, CSRF.
- Auth : mots de passe hachés (Argon2 ou bcrypt), tokens à durée limitée, MFA proposé si pertinent.
- Autorisations : principe du moindre privilège, contrôle d'accès vérifié côté serveur.
- Rate limiting sur login et endpoints sensibles.
- CORS restreint aux domaines nécessaires.
- Secrets : `.env` ignoré par Git + `.env.example` fourni + scan de secrets (ex. gitleaks) en pré-commit et en CI.
- Audit des dépendances automatisé (Dependabot/Renovate + `npm audit` ou équivalent).
- Logs d'audit sur les actions sensibles, **sans données personnelles en clair**.
- Documente tout dans `docs/SECURITY.md`.

### 5.5 RGPD (si des données personnelles sont traitées)
- Cartographie des données : quelles données, pourquoi, où, combien de temps (`docs/RGPD.md`).
- **Minimisation** : ne collecter que le nécessaire.
- Base légale identifiée pour chaque traitement (consentement, contrat, intérêt légitime…).
- Hébergement des données **dans l'UE** (ou garanties adéquates) — signale si un service choisi ne le permet pas.
- Consentement explicite, bandeau cookies conforme si trackers non essentiels.
- Fonctionnalités à prévoir : **export des données**, **suppression du compte et des données**, rectification.
- Durées de conservation définies + purge automatique.
- Chiffrement en transit (TLS) et au repos pour les données sensibles.
- Politique de confidentialité et mentions légales à rédiger (signale ce qui nécessite un avis juridique : tu n'es pas juriste).
- Procédure en cas de fuite de données (notification CNIL sous 72 h) dans le RUNBOOK.
- Sous-traitants (hébergeur, email, analytics) listés avec leur DPA.

### 5.6 Qualité de code
- Linter + formateur automatiques, pré-commit hooks.
- Typage strict si le langage le permet.
- Fonctions courtes, une responsabilité, noms explicites, pas de code dupliqué.
- Gestion d'erreurs centralisée, pas d'échec silencieux, messages clairs (utilisateur ≠ logs).
- Zéro warning au build.
- Dépendances minimales, versions verrouillées (lockfile).

### 5.7 Accessibilité & UX
- Mobile-first, responsive.
- Accessibilité **WCAG 2.1 AA** (RGAA si public français concerné) : contrastes, navigation clavier, labels, zones cliquables ≥ 44 px.
- États de chargement, d'erreur et de vide gérés sur chaque écran.

### 5.8 Performance
- Lighthouse cible : 90+ (si web).
- Lazy loading, images optimisées, budget de taille de bundle.
- Index en base sur les colonnes recherchées, pas de requêtes N+1.
- Mesure avant d'optimiser.

### 5.9 Observabilité & exploitation
- Logs structurés (JSON, niveau, contexte).
- Suivi d'erreurs (ex. Sentry) + alertes sur erreurs critiques.
- Healthcheck + monitoring de disponibilité.
- **Sauvegardes automatiques de la base**, rétention définie, **test de restauration documenté**.

### 5.10 Documentation (`/docs`, mise à jour en continu)
- `README.md` : installation, lancement, tests, déploiement
- `ARCHITECTURE.md` : stack + diagramme + raisons des choix
- `DECISIONS.md` : journal des décisions (date, raison)
- `API.md` (si backend) : endpoints, auth, exemples
- `DATABASE.md` : schéma, migrations, données sensibles
- `DEPLOYMENT.md` : environnements, CI/CD, rollback
- `SECURITY.md` et `RGPD.md`
- `RUNBOOK.md` : problèmes rencontrés + solutions
- `CONTRIBUTING.md` : workflow, checklist PR
- `CHANGELOG.md`
- `PLAN_DEVELOPPEMENT.md` : jalons, tâches, risques, hors périmètre (voir section 6)

---

## 6. PHASE 3 — PLAN DE DÉVELOPPEMENT

Une fois la stack validée, produis `docs/PLAN_DEVELOPPEMENT.md`, puis **attends ma validation**.

Contenu attendu :

1. **Jalons (milestones)** dans l'ordre :
   - J0 : socle (repo, CI, lint, tests, environnements, docs de base, sécurité de base)
   - J1 : premier parcours utilisateur complet, même minimal (« walking skeleton » déployé en staging)
   - J2+ : une fonctionnalité MVP par jalon
   - J-final : durcissement (sécurité, RGPD, accessibilité, perf, sauvegardes) + mise en production
2. **Pour chaque jalon** :
   - objectif en 1 phrase
   - liste de tâches numérotées, petites (≤ 1/2 journée chacune)
   - critères d'acceptation (comment je vérifie que c'est fini)
   - tests à écrire
   - points sécurité / RGPD concernés
   - dépendances (ce qui doit être fait avant)
   - estimation (S / M / L) — **indique ton niveau d'incertitude**
3. **Risques** : top 5 (technique, légal, dépendance externe) + parade.
4. **Hors périmètre** : liste explicite de ce qui est reporté en v2+.
5. **Ordre de priorité** si je dois couper du scope.
6. **Suivi** : crée les tâches sous forme d'issues (GitHub/GitLab) rattachées aux jalons, et garde le plan à jour.

---

## 7. PHASE 4 — DÉVELOPPEMENT

1. Suis le plan, **un jalon à la fois**, tâche par tâche.
2. Pour chaque tâche : branche → code + tests → docs → PR → CI verte → merge.
3. À la fin de chaque tâche, résume en **3 lignes max** : ce qui est fait, ce qui reste, ce qui bloque.
4. À la fin de chaque jalon : démo/check des critères d'acceptation + mise à jour de `PLAN_DEVELOPPEMENT.md`, `CHANGELOG.md` et `DECISIONS.md`.
5. Signale immédiatement tout écart au MVP (« ceci est de la v2 ») ou au plan, et propose un ajustement avant de continuer.

---

## 8. DÉFINITION DE « TERMINÉ »

- [ ] Tous les jalons du plan livrés, critères d'acceptation validés
- [ ] Fonctionnalités MVP livrées et testées
- [ ] Tests unitaires, intégration et e2e verts en CI
- [ ] Aucun secret dans le repo, audit dépendances propre
- [ ] Checklist sécurité (5.4) et RGPD (5.5) cochée, points ouverts listés
- [ ] Accessibilité et performance vérifiées
- [ ] Sauvegardes et rollback testés
- [ ] `/docs` complète et synchronisée
- [ ] Historique Git lisible
- [ ] Liste des points incertains ou à valider avec un juriste/expert

---

## 9. NOTES COMPLÉMENTAIRES

[Contraintes spécifiques, APIs externes, deadlines...]

---

## Historique des versions
Règle : toute modification du prompt met à jour ce fichier, augmente la version et ajoute une ligne ici. Le détail exact est dans l'historique git (`git log -p "2 - Prompt app claude.md"`).

| Version | Date | Modifications |
|---|---|---|
| 1.0.0 | 2026-10-27 | Première version : reprise du prompt base Claude Code, réécrit pour que Claude Code choisisse les technologies (phase 1) et applique les bonnes pratiques (tests automatisés, pull requests, sécurité, RGPD, CI/CD, accessibilité, observabilité, documentation), avec un plan de développement par jalons (phase 3) avant le développement (phase 4). |
