# 2 - Prompt app claude : choix des technologies, bonnes pratiques et plan de développement

> Version 1.1.1 (2026-10-27). Historique des modifications en fin de fichier.

> Ce prompt s'exécute avec les livrables du prompt « 1 - Prompt idée app » : **il n'y a rien à remplir**.
> Claude Code lit ces livrables dans le dépôt, choisit la stack, applique les bonnes pratiques et produit le plan de développement.
> Pré-requis : les livrables du prompt 1 sont dans `docs/` du dépôt de travail (voir section 1).

---

## 1. ENTRÉES : LIVRABLES DU PROMPT 1

Le produit est déjà conçu. Ne me demande pas de le redécrire : lis-le.

**Au démarrage, avant toute autre action :**
1. Liste `docs/` (dépôt de travail) et repère les livrables du prompt 1, même si leurs noms diffèrent : identifie-les par leur contenu.
2. Lis-les en entier. Ordre de priorité si deux informations se contredisent : **description complète du produit > brief > fiche projet > reste**. Signale-moi toute contradiction, sans trancher seul.
3. Affiche un **récapitulatif d'entrée** (20 lignes max) : ce que tu as trouvé, ce que tu en retiens, ce qui manque.

**Livrables attendus et ce que tu en tires :**

| Livrable du prompt 1 | Ce que tu en tires |
|---|---|
| Description complète du produit (versions v1 → finale) | Périmètre : **v1 = MVP**, versions suivantes = v2+ ; critères de passage entre versions ; liste des fonctionnalités avec priorité et persona |
| Brief produit | Vision, cibles, proposition de valeur, modèle économique, nom validé |
| FICHE PROJET (dernière version) | Décisions prises, hypothèses à valider, plateforme, contraintes (budget, temps, compétences, RGPD), chiffres de succès, questions ouvertes |
| Userflow, story mapping | Parcours et user stories à découper en tâches ; cas particuliers (erreur, premier lancement, abonnement) |
| Wireframes | Liste des écrans, navigation, états à développer |
| Direction artistique + charte graphique | Design tokens (couleurs, typo, espacements), composants, thème clair/sombre, niveau d'accessibilité |
| Journal des décisions | Décisions déjà actées : ne les remets pas en cause sans me le dire |

**Si des livrables manquent ou si `docs/` est vide :** liste ce qui manque, dis-moi lesquels sont bloquants, et propose : (A) relancer le prompt 1, (B) continuer avec des hypothèses que tu listes. Ne code rien tant que je n'ai pas choisi.

---

## 2. RÈGLES DE FONCTIONNEMENT

- **Source de vérité = fichiers du repo (`/docs`)**, pas la conversation. À chaque démarrage : relis `/docs`, y compris les livrables du prompt 1.
- **Ne redéfinis pas le produit** : les décisions produit (cibles, fonctionnalités, versions, nom, DA) viennent du prompt 1. Si une contrainte technique ou légale les remet en cause, dis-le et propose une alternative, sans modifier seul.
- Mets à jour `/docs` à **chaque décision, changement ou blocage résolu**.
- **Un seul journal des décisions** : réutilise celui créé par le prompt 1 ou par le prompt 3 (`docs/decisions.md`, format DEC-xx : une décision = une entrée datée, la plus récente en haut), n'en crée pas un second. `DECISIONS.md` ci-dessous désigne ce journal. Si les fichiers du starter pack existent (`AGENTS.md`, `docs/now.md`…), tiens-les à jour selon le contrat de maintenance d'`AGENTS.md` : stack et commandes dans `AGENTS.md`, backlog dans `docs/now.md` (qui renvoie vers `docs/PLAN_DEVELOPPEMENT.md`).
- **Si tu n'es pas sûr d'une info** (version, prix, compatibilité, obligation légale) : dis-le explicitement et vérifie via recherche web avant de recommander.
- **Challenge mes hypothèses.** Si une demande est floue, hors MVP ou risquée : dis-le.
- Réponses courtes, concrètes, étape par étape. Pas de pavés théoriques.

---

## 3. PHASE 0 — QUESTIONS (avant toute proposition)

Avant de proposer une stack, pose-moi **au maximum 8 questions** (une liste numérotée, courte), **uniquement sur ce que les livrables du prompt 1 ne disent pas**. Ne repose jamais une question dont la réponse est dans `docs/`.

Sujets à vérifier d'abord dans les livrables, puis à demander seulement s'ils manquent :
- volumétrie attendue (utilisateurs, données) : à déduire des critères de passage entre versions
- données personnelles / sensibles (RGPD)
- besoin hors-ligne, temps réel, notifications, paiement, IA
- budget d'hébergement mensuel
- compétences que je veux garder (ce que je sais maintenir)

Pour chaque question, donne 3 à 4 options avec ta recommandation, et accepte « je ne sais pas » (tu prends l'option recommandée et tu la notes comme hypothèse à valider).
Si tout est déjà dans `docs/`, dis-le et passe à la phase 1 après mon « ok ». Ne code rien à ce stade.

---

## 4. PHASE 1 — CHOIX DES TECHNOLOGIES

Pour **chaque couche utile** (frontend, backend, base de données, auth, hébergement, CI/CD, monitoring, tests, paiement/email/stockage si besoin) :

1. Propose **2 à 3 options** réalistes, adaptées à la plateforme, aux contraintes et au modèle économique des livrables du prompt 1.
2. Compare-les dans un tableau court selon ces critères :
   - adéquation au produit, au MVP (v1) et aux versions suivantes (pas de choix qui bloque la v2+)
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

Le plan se construit à partir de la description complète du produit : **le découpage en versions (v1, v2, v3…) du prompt 1 est la structure du plan**.

Contenu attendu :

0. **Correspondance avec le prompt 1** : tableau fonctionnalité → version → jalon(s) → écrans des wireframes. Aucune fonctionnalité de la v1 ne doit être oubliée, aucune fonctionnalité de v2+ ne doit s'infiltrer dans la v1.
1. **Jalons (milestones)** dans l'ordre :
   - J0 : socle (repo, CI, lint, tests, environnements, docs de base, sécurité de base, design tokens issus de la charte graphique)
   - J1 : premier parcours utilisateur complet, même minimal (« walking skeleton » déployé en staging), tiré du userflow
   - J2+ : une fonctionnalité de la v1 par jalon, par ordre de priorité du story mapping
   - J-final de la v1 : durcissement (sécurité, RGPD, accessibilité, perf, sauvegardes) + mise en production
   - Versions suivantes (v2, v3… jusqu'à la version finale) : jalons au niveau « épopée » seulement (objectif, fonctionnalités, critère de déclenchement repris du prompt 1, dépendances techniques à anticiper). Le détail tâche par tâche se fait quand la version est déclenchée.
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
- [ ] Fonctionnalités de la v1 (MVP) livrées et testées, conformes à la description du produit et aux wireframes
- [ ] Interface conforme à la charte graphique
- [ ] Tests unitaires, intégration et e2e verts en CI
- [ ] Aucun secret dans le repo, audit dépendances propre
- [ ] Checklist sécurité (5.4) et RGPD (5.5) cochée, points ouverts listés
- [ ] Accessibilité et performance vérifiées
- [ ] Sauvegardes et rollback testés
- [ ] `/docs` complète et synchronisée
- [ ] Historique Git lisible
- [ ] Liste des points incertains ou à valider avec un juriste/expert
- [ ] Plan de la version suivante (v2) préparé, avec son critère de déclenchement

---

## 9. NOTES COMPLÉMENTAIRES

[Contraintes spécifiques, APIs externes, deadlines...]

---

## Historique des versions
Règle : toute modification du prompt met à jour ce fichier, augmente la version et ajoute une ligne ici. Le détail exact est dans l'historique git (`git log -p "2 - Prompt app claude.md"`).

| Version | Date | Modifications |
|---|---|---|
| 1.1.1 | 2026-10-27 | Cohérence avec le prompt 3 : le journal des décisions unique est `docs/decisions.md` (format DEC-xx) ; si les fichiers du starter pack existent, ils sont tenus à jour selon le contrat de maintenance d'`AGENTS.md`. |
| 1.1.0 | 2026-10-27 | Le prompt s'exécute avec les livrables du prompt 1 : plus rien à remplir. Section 1 remplacée par la lecture de `docs/` (récapitulatif d'entrée, ordre de priorité en cas de contradiction, comportement si des livrables manquent) ; questions de la phase 0 limitées à ce qui manque ; plan de développement structuré par les versions v1 → finale du prompt 1 (v1 détaillée, versions suivantes en épopées) avec table de correspondance fonctionnalité → version → jalon → écran ; journal des décisions unique partagé avec le prompt 1 ; charte graphique et wireframes dans la définition de « terminé ». |
| 1.0.0 | 2026-10-27 | Première version : reprise du prompt base Claude Code, réécrit pour que Claude Code choisisse les technologies (phase 1) et applique les bonnes pratiques (tests automatisés, pull requests, sécurité, RGPD, CI/CD, accessibilité, observabilité, documentation), avec un plan de développement par jalons (phase 3) avant le développement (phase 4). |
