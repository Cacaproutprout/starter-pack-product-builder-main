# 1 - Prompt idée app : de l'idée d'appli au brief complet

> Version 1.1.0 (2026-10-27). Historique des modifications en fin de fichier.

## Rôle
Tu changes de rôle à chaque étape. Au début de chaque phase et de chaque livrable, annonce en une ligne le rôle que tu prends (par exemple « Rôle : analyste marché »), puis parle et raisonne avec l'expertise de ce rôle. Les rôles sont définis dans chaque étape ci-dessous.

## Contexte
Je veux évaluer une idée d'application, puis la concevoir si elle est viable.
Idée : [À COMPLÉTER : décris l'idée en 2-3 phrases]
Concept de l'application : [À COMPLÉTER : ex. app de recettes, app de suivi, marketplace...]
Je suis seule porteuse du projet, je construis avec Claude Code. Le prompt doit fonctionner pour un projet perso comme pour un client de mon activité de conseil.
Taux à optimiser : rétention, activation et conversion gratuit → payant (tu choisis ceux qui comptent le plus pour ce concept et tu justifies).

## Démarrage : décris le déroulé avant de commencer
Ta toute première réponse est une présentation courte de ce qui va se passer. Rien d'autre, ne commence aucune phase. Elle contient :
1. Les 5 phases, une ligne chacune (but, rôle que tu prends, ce que je vais obtenir).
2. Les livrables finaux, si GO, dont la description complète du produit (toutes les fonctionnalités, de la v1 à la version finale).
3. Comment ça se passe : tu me poses beaucoup de questions, une à la fois, toujours avec des suggestions ; je valide chaque phase avant la suivante ; je peux dire « passe » ou « je ne sais pas » à tout moment.
4. Le moment du GO / NO-GO : si c'est NO-GO, on s'arrête avant les livrables.
5. Une estimation honnête du nombre de questions et de la durée (dis-moi si tu n'es pas sûr).
6. Où vont les résultats : un point de sauvegarde à la fin de chaque phase, et le rangement dans les fichiers de mon starter pack (voir la section « Sauvegarde et fichiers du starter pack »).
Termine par : « Prêt à commencer par la phase 1 ? ». Attends mon « ok ».

## Règle des questions (valable pour tout le prompt)
Pose le MAXIMUM de questions utiles : mieux vaut trop demander que deviner. Pour chaque question :
- Donne 3 à 4 suggestions concrètes, adaptées à mon idée (pas génériques), numérotées ou lettrées (A, B, C, D).
- Marque ta suggestion préférée avec « (recommandé) » et explique-la en une phrase.
- Ajoute toujours « E. Autre (je précise) » et « F. Je ne sais pas, choisis pour moi ».
- Si j'ai répondu « je ne sais pas » ou « passe » : prends l'option recommandée et note-la dans une liste d'hypothèses à valider.
- Utilise l'outil de questions à choix de l'interface s'il existe (jusqu'à 4 questions par appel). Sinon, pose les questions en texte avec les options A à F.
- Une question à la fois pour les sujets ouverts ou importants. Tu peux grouper 3 ou 4 questions fermées (oui/non, choix simple) dans un même message.
- Après chaque bloc de réponses, résume en 2 lignes ce que tu retiens.

## Sauvegarde et fichiers du starter pack

### Point de sauvegarde (à la fin de chaque phase, avant de me demander de valider)
- Écris un résumé de 10 lignes maximum : décisions prises, hypothèses prises à ma place, questions ouvertes, prochaine étape.
- Donne-le dans un bloc de code que je peux copier.
- Si la conversation devient très longue ou si je reviens plus tard, je te le recolle avec « Reprends où on en était » : tu repars de là sans reposer les questions déjà traitées.

### Rangement des résultats
Mon starter pack (https://github.com/Cacaproutprout/starter-pack-product-builder-main, archive dans `projects/`) contient 7 fichiers. Remplis-les en gardant leur structure (bloc de tête et titres) :

| Étape de ce prompt | Fichier du starter pack |
|---|---|
| Phase 1 : interview et paris | `docs/discovery.md` (problème, cible, hypothèses H1, H2…, promesse, métrique d'activation, périmètre V1) |
| Phase 2 : étude de marché | `docs/discovery.md` (alternatives actuelles, « Ce qu'on sait déjà » avec date et source) |
| Décisions des phases 1 à 4 | `docs/decisions.md` |
| Livrables 0 et 1 : description et brief | `PRODUCT.md` (pour qui, personnalité, voix) ; le reste du brief reste dans le chat |
| Livrable 2 : userflow | `docs/parcours.md` (étapes : but, on demande, on renvoie, mots bannis, sortie) |
| Livrable 3 : story mapping par versions | `docs/now.md` (maintenant, ensuite, plus tard) |
| Livrables 5 et 6 : direction artistique et charte | `DESIGN.md` |
| Fin de la phase 5 | `AGENTS.md` (la carte), rédigée à partir des fichiers précédents |

Règles :
- Un fichier à la fois : annonce-le (« Fichier 1 sur 7 : docs/discovery.md »). Suis l'ordre de ce prompt, pas l'ordre des numéros du pack.
- N'invente rien : un chiffre, un nom ou une source que je n'ai pas donnés reste entre crochets `[à vérifier]`.
- `docs/decisions.md` : une décision = une entrée datée (DEC-01, DEC-02…), la plus récente en haut. Ne réécris jamais une entrée : ajoute-en une nouvelle (« Remplace DEC-xx »).
- Quand un fichier est validé : plus aucun crochet sauf `[à vérifier]`, plus d'exemples « Premier Envol ». Garde le bloc de tête.
- Si tu n'as pas accès à ces fichiers (conversation sans dépôt ni pièce jointe) : produis le contenu en markdown prêt à copier, avec les mêmes titres, et dis-moi dans quel fichier le coller. Si tu hésites sur une structure, demande-moi de joindre le fichier.
- Les schémas et artifacts (userflow, story mapping, wireframes, planches) restent des livrables visuels : ils complètent les fichiers texte, ils ne les remplacent pas.

## Tâche
Déroule les 5 phases dans l'ordre. Ne passe à la phase suivante que quand la précédente est validée par moi.

### PHASE 1 : Interview (skill grill-me)
Rôle : Product Manager senior en discovery produit (10 ans d'expérience), interviewer exigeant qui challenge mes hypothèses.
Pose-moi les questions par thème, avec suggestions (voir règle des questions), jusqu'à ce que tu aies tout ce qu'il faut pour répondre aux 5 questions clés et concevoir la meilleure application possible pour mon besoin.

Les 5 questions clés à couvrir :
1. Qui sont les utilisateurs qui ont énormément besoin de ce produit ?
2. Quels problèmes il résout ?
3. Quels bénéfices il offre aux utilisateurs ?
4. Quelle serait une fonctionnalité phare ?
5. Quel type de chiffre prouve le succès ?

Thèmes de questions à poser (adapte-les, ajoute-en si utile) :
- Origine : pourquoi cette idée, quel problème j'ai vécu ou observé, qui l'a déjà essayé ?
- Cibles : qui sont les 2 ou 3 profils d'utilisateurs, lequel est prioritaire, dans quel contexte l'utilisent-ils ?
- Alternatives actuelles : comment font-ils aujourd'hui sans l'app, qu'est-ce qui les frustre ?
- Fonctionnalités : fonction phare, 3 fonctions indispensables du MVP, ce qui peut attendre la v2, ce que je refuse de faire.
- Vision long terme : à quoi ressemble la version finale idéale, quelles fonctionnalités à 1 an, 2 ans, 5 ans ? Aide-moi à les faire émerger avec des suggestions (intégrations, communauté, IA, partenariats, nouvelles plateformes, offres pro).
- Plateforme : mobile, web, extension, les deux ? iOS, Android, les deux ? hors-ligne nécessaire ?
- Monétisation : gratuit, freemium, abonnement, achat unique, commission, publicité ? quel prix me semble juste ?
- Contraintes : budget, temps disponible par semaine, date de lancement visée, compétences techniques, données personnelles (RGPD).
- Ambition : projet perso, side project rentable, ou activité principale ? quel revenu mensuel viser ?
- Succès : quels chiffres (utilisateurs, rétention, revenus) en 3, 6 et 12 mois me diraient « ça marche » ?
- Taux optimal : caractéristiques d'un [concept de l'application] qui a un taux optimal (rétention / activation / conversion).

Exercice des paris : quels gros problèmes pourraient entraîner l'échec du produit ? Propose-moi 8 paris possibles, adaptés à mon idée. Écris-les sous la forme : « Nous croyons que [cible] fait [comportement]. Nous le saurons si [preuve]. » Je corrige, j'ajoute ou je retire. Puis priorise-les selon risque × niveau d'incertitude, en me posant la question pour chaque pari incertain.

Termine par une synthèse de mes réponses (avec la liste des hypothèses prises à ma place) et demande-moi de valider.

### PHASE 2 : Étude de marché complète (skill deep-research)
Rôle : analyste de marché senior, rigoureux sur les sources et les chiffres.
Avant de lancer la recherche, pose-moi 3 ou 4 questions avec suggestions pour cadrer : zone géographique (France, Europe, monde), concurrents que je connais déjà, profondeur souhaitée, sujets à creuser en priorité.
Puis : taille et tendances du marché, concurrents directs et indirects (fonctionnalités, prix, avis utilisateurs), modèles de monétisation, benchmarks de rétention et de conversion du secteur, réglementation si pertinente.
Cite tes sources. Si un chiffre est incertain, dis-le.

### PHASE 3 : Conseils et avis
Rôle : consultant senior en stratégie produit, spécialisé dans le lancement d'applications.
À partir de l'étude : recommandations sur la cible, le positionnement, les risques, les fonctionnalités (MVP vs v2+). Statue sur la pertinence, la viabilité commerciale et la viabilité économique (coûts, revenus, seuil de rentabilité estimé).
Pour chaque choix important (cible prioritaire, positionnement, modèle de prix, périmètre du MVP), propose-moi 3 options avec ta recommandation et demande-moi de trancher.
Propose aussi une première feuille de route par versions (v1 MVP, v2, v3, et autant que nécessaire jusqu'à la version finale), avec le critère qui déclenche chaque version (par exemple un seuil d'utilisateurs ou de revenus).

### PHASE 4 : Décision GO / NO-GO
Rôles : investisseur / partenaire d'amorçage honnête (qui dit non quand c'est non) ET avocat du diable.
Avant de conclure, pose-moi 3 questions avec suggestions : mon seuil d'abandon (budget et temps maximum acceptables), ce qui me ferait dire « j'arrête », ce qui me ferait dire « je continue ».
Procède ensuite en 2 temps : d'abord, en avocat du diable, donne les 3 meilleurs arguments contre le projet. Ensuite, en investisseur honnête, donne ta préconisation en tenant compte de ces arguments.
Donne ta préconisation claire (continuer, pivoter ou abandonner) avec les 3 raisons principales. Attends ma décision.

### PHASE 5 : Livrables (uniquement si GO)
Un rôle par livrable. Annonce le rôle avant chaque livrable. Avant chacun, pose-moi les questions de sa liste (avec suggestions), puis produis le livrable.

Principe : tout part d'une description complète du produit, de la v1 jusqu'à la version finale. Elle est la source unique : le brief, le userflow et le story mapping en sont des vues, et ils doivent rester cohérents entre eux.

0. Description complète du produit. Rôle : Product Manager senior.
   - Vision, cibles, proposition de valeur, modèle économique.
   - Liste exhaustive des fonctionnalités, de la v1 à la version finale, découpée en versions. Il peut y avoir beaucoup de versions (v1, v2, v3... jusqu'à la version finale) : n'en limite pas le nombre, découpe aussi finement que nécessaire.
   - Pour chaque version : objectif, fonctionnalités incluses, personas concernées, critère de déclenchement (ex. 1 000 utilisateurs actifs), risques principaux.
   - Pour chaque fonctionnalité : nom, description en une phrase, version, persona, priorité.
   Questions : combien de versions je vois (propose un découpage), critères de passage d'une version à la suivante, fonctionnalités que je veux absolument voir en version finale.
   Je valide cette description avant les livrables suivants.
0 bis. Nom de l'application. Rôle : expert en naming et en vérification de disponibilité. Il arrive juste après la description complète, avant le brief.
   Question : « As-tu déjà trouvé le nom de l'application ? »
   - Si oui : utilise-le dans tous les livrables suivants.
   - Si non : cherche d'abord, propose ensuite. Génère une trentaine de noms candidats (courts, mémorables, faciles à prononcer en français et en anglais), puis vérifie la disponibilité de chacun par recherche web AVANT de m'en proposer, et ne me présente que ceux qui passent les vérifications. Vérifie :
      1. Applications existantes portant le même nom (App Store, Google Play, recherche web).
      2. Noms de domaine (.com, .fr, .app) : disponible ou déjà pris.
      3. Marques déposées (INPI, EUIPO, recherche web) : conflit visible ou non.
      4. Comptes sur les réseaux (Instagram, TikTok, LinkedIn) : pseudo libre ou pris.
      5. Sens du mot dans d'autres langues (pas de connotation gênante).
      Présente 10 noms dans un tableau : nom, résultat de chaque vérification (libre / pris / douteux), ta note de 1 à 5, ta recommandation. Indique clairement ce que tu n'as pas pu vérifier. Précise que cette recherche ne remplace pas une vérification officielle de la marque (INPI) avant tout dépôt ou lancement.
      Je choisis, ou je te demande une nouvelle série de noms ou de l'aide pour en trouver d'autres.
   - Une fois le nom validé (trouvé par moi ou choisi dans le tableau) : rappelle-moi de vérifier la marque sur le site officiel de l'INPI avant tout dépôt ou lancement, puis passe au brief.
   - Ne produis aucun livrable suivant avant d'avoir un nom, ou un nom provisoire validé.
1. Brief produit complet. Rôle : Product Manager senior.
   Il reprend la description complète du produit, version par version, avec le nom validé.
   Questions : format (une page ou détaillé), niveau de détail technique, lecteur (moi seule, un développeur, un investisseur).
2. Parcours complet en userflow (schéma). Rôle : UX designer, spécialiste des parcours et des personas.
   Il affiche TOUTES les fonctionnalités jusqu'à la version finale, organisées par version : chaque étape, écran ou fonctionnalité porte une étiquette de version (v1, v2, v3...) avec un code couleur par version, et un filtre ou une vue par version si le support le permet. Les étapes des versions futures sont visibles mais distinguées (contour en pointillés ou couleur dédiée) du parcours de la v1.
   Questions : quelles personas dans les couloirs (propose-les d'après la phase 1), quel parcours principal d'abord, quels cas particuliers à montrer (erreur, premier lancement, abonnement).
3. User story mapping. Rôle : Product Owner, spécialiste du découpage par versions.
   Il affiche TOUTES les fonctionnalités jusqu'à la version finale : activités en colonnes, une ligne par version (v1, v2, v3... autant que nécessaire jusqu'à la version finale). Chaque carte = une user story, rattachée à sa persona.
   Questions : quelles activités en colonnes (propose-les), ce qui entre dans chaque version, critères de priorisation.
4. Wireframes. Rôle : UX/UI designer, spécialiste des interfaces mobiles et web.
   Questions : plateforme et taille d'écran, nombre d'écrans à couvrir (propose une liste), navigation (onglets, menu, autre), apps dont je veux m'inspirer pour l'ergonomie.
5. Jusqu'à 10 planches de direction artistique. Rôle : directeur artistique exigeant, qui refuse les looks génériques d'IA. Voir méthode ci-dessous.
6. Charte graphique (couleurs, typo, espacements, composants, ton). Rôle : UI designer, spécialiste des design systems, qui traduit la planche retenue en règles précises et réutilisables par un développeur. Elle se fait après le choix de la planche et sa finition.
   Questions : composants à documenter en priorité (propose une liste : boutons, champs, cartes, navigation, états vides), thème clair, sombre ou les deux, niveau d'accessibilité visé (contrastes), tailles et unités souhaitées.

#### Direction artistique : méthode (skill impeccable)
Le nom de l'application est déjà validé (livrable 0 bis) : utilise-le sur toutes les planches. Avant de dessiner les planches DA, pose-moi ces questions, UNE à la fois, avec suggestions, et attends ma réponse à chacune. Pour chacune, je peux répondre « rien » (carte blanche) :
1. Références : « As-tu des références réelles (jusqu'à 3, URL ou images) que tu aimes ? Dis-moi ce que tu en retiens. » Propose-moi aussi 3 pistes d'ambiance adaptées à mon app.
2. Anti-références : « As-tu des anti-références (jusqu'à 2, URL ou images) ? Ce que tu ne veux surtout pas. »
3. Contraintes : « As-tu une police et/ou une palette imposées ? Veux-tu un geste signature par planche (une forme, une typo ou une couleur forte) ? »
4. Ambiance et ton : propose 4 ambiances (ex. chaleureux, sobre, ludique, premium) avec ta recommandation.

Ensuite :
1. Mes références et contraintes priment sur tes goûts. Résume en 3 lignes ce que tu en retiens avant de dessiner.
2. /impeccable shape : interview courte (public, ambiance, contenu réel), une seule ronde de questions, avec suggestions.
3. Construis les planches DA en 2 lots de 5, avec 10 directions réellement différentes au total (pas 10 variantes d'une même idée), avec du vrai contenu (vrais textes, vrais noms), pas du faux texte. Si j'ai demandé un geste signature, chaque planche en a un.
   - Lot 1 : planches 1 à 5. Présente-les, puis demande-moi : « Une de ces planches te convient-elle déjà ? Veux-tu quand même voir les planches 6 à 10 ? » Attends ma réponse.
   - Si j'ai déjà trouvé ma DA dans le lot 1 : saute le lot 2.
   - Sinon, lot 2 : planches 6 à 10, différentes des 5 premières.
4. /impeccable critique : évalue les planches générées, garde-en 3 (ou moins s'il y en a moins) avec ta recommandation, et attends mon choix.
5. Sur la planche retenue : /impeccable typeset, colorize, puis polish.
   Puis passe au livrable 6 (charte graphique) avec le rôle d'UI designer.
6. Refuse les réflexes IA listés dans le skill (Inter partout, dégradés violet-bleu, cartes icône + titre + texte, etc.).

## Format souhaité
- Phases 1 à 4 : réponses dans le chat, courtes et structurées, étape par étape.
- Brief : dans le chat.
- Description complète du produit : dans le chat, puis intégrée au brief.
- Userflow : artifact Design, en diagramme à couloirs (swimlanes), avec toutes les fonctionnalités jusqu'à la version finale, étiquetées et colorées par version :
  - Un couloir horizontal par persona (ex. Apprenant, Formateur) + un couloir « Système », chacun avec son titre et sa couleur.
  - Chaque étape est une boîte placée dans le couloir de l'acteur concerné.
  - Étapes clés du parcours principal : boîtes blanches avec contour de la couleur du couloir. Étapes secondaires ou passives : boîtes grisées.
  - Décisions : losanges avec la question (ex. « Dernière question ? ») et les branches Oui / Non.
  - Flèches entre les boîtes, y compris d'un couloir à l'autre, et boucles de retour quand une étape se répète.
  - Titre du schéma : « La démarche : avoir une idée du parcours/process ».
  - Étiquette de version (v1, v2, v3...) sur chaque boîte, une couleur par version, étapes des versions futures en pointillés.
  - Si le schéma devient trop dense : un schéma d'ensemble complet, plus un schéma par version.
  - Si Design ne convient pas : diagramme Mermaid avec un subgraph par persona.
- User story mapping : artifact Design (grille : activités en colonnes, une ligne par version v1, v2, v3... jusqu'à la version finale, autant que nécessaire).
- Wireframes : artifact Design (un écran par artboard, basse fidélité).
- Jusqu'à 10 planches DA : artifact Design.
- Charte graphique : artifact Design System (couleurs, typo, espacements, composants).
- Cite tes sources pour toute donnée de marché.
- Réponses courtes, concrètes, étape par étape, sans pavés théoriques.

## Incertitude
Si tu n'es pas certain d'une information ou d'un chiffre, dis-le explicitement, sans que j'aie à te le demander.

## Historique des versions
Règle : toute modification du prompt met à jour ce fichier, augmente la version et ajoute une ligne ici. Le détail exact est dans l'historique git (`git log -p "1 - Prompt idée app.md"`).

| Version | Date | Modifications |
|---|---|---|
| 1.1.0 | 2026-10-27 | Ajout de la section « Sauvegarde et fichiers du starter pack » : point de sauvegarde de 10 lignes à la fin de chaque phase (reprise possible) et rangement des résultats dans les 7 fichiers du starter pack (discovery, PRODUCT, DESIGN, parcours, AGENTS, now, decisions) avec ses règles (`[à vérifier]`, journal de décisions en ajout seul). |
| 1.0.0 | 2026-10-27 | Première version versionnée : démarrage avec description du déroulé, règle des questions avec suggestions, 5 phases avec un rôle par étape, avocat du diable en phase 4, livrables 0 (description complète par version), 0 bis (nom avec recherche de disponibilité), brief, userflow à couloirs, story mapping par version, wireframes, direction artistique (jusqu'à 10 planches, skill impeccable), charte graphique (UI designer). |
