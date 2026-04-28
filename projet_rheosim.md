
RHEOSIM
ENTERPRISE

Plateforme Scientifique de Simulation Visco-Élastique
Cahier des charges produit — Édition exécutable v3.0
Vision produit • Architecture détaillée • Trade-offs • UX • Data • Go-To-Market
Document	Cahier des charges produit — Édition exécutable v3.0
Nature	Vision + Architecture + ADR + UX + Data + GTM + Critique
Audience	Développeurs, scientifiques, décideurs, investisseurs, partenaires
Date	Avril 2026
Statut	Référence interne — prêt pour exécution projet

« From Lab Data to Digital Prediction »
 
TABLE DES MATIÈRES
1.  Résumé Exécutif
Core Innovation Statement   ✦ NEW v3
Présentation — Vision — Positionnement — Proposition de valeur
2.  Problématique
Problème résolu — Importance — Limites existantes — Enjeux
3.  Vision Produit
Description — Personas — Cas d'usage — Workflow UX
§3.5 UX concrète : description des 5 écrans principaux   ✦ NEW v3
4.  Différenciation & Innovation
9 innovations défendables — 5 idées gadgets à éviter
5.  Architecture Conceptuelle
Vue globale — Modules — Flux — Jobs — Communication
§5.6 Décisions d'architecture (ADR) — 5 trade-offs documentés   ✦ NEW v3
§5.7 Diagrammes complémentaires (microservices, flux, FEM, lifecycle)   ✦ NEW v3
6.  Architecture Scientifique
Modèles — Expériences — FEM/FVM — Variables internes — Pipeline — Validation
7.  Roadmap
V1 MVP — V2 Avancée — V3 Vision long terme
§7.6 Scope technique du compute engine V1 (inclus / exclus)   ✦ NEW v3
8.  Document Technique
Stack — Modules C++ — Formats — Pipeline — Risques — Recommandations
§8.8 Stratégie de données (sources, format, versionning, IA)   ✦ NEW v3
9.  Document Non Technique
Description simple — Bénéfices — Avantages — Impact — Vision 5 ans
§9.7 Stratégie Go-To-Market en 3 phases progressives   ✦ NEW v3
10.  Critique Experte
Faiblesses — Risques — Erreurs à éviter — Recommandations — GO conditionnel
 
PARTIE 1 — Résumé Exécutif
🎯 Core Innovation Statement
RheoSim Enterprise est la première plateforme intégrée qui transforme l'identification visco-élastique d'un travail d'expert de plusieurs jours en un workflow reproductible de quelques minutes — en réunissant pour la première fois données expérimentales, modèles physiques rigoureux, intelligence artificielle native et simulation 3D dans un environnement unique, ouvert, et scientifiquement vérifiable.

Tout le reste de ce document découle de cette ambition. Chaque choix d'architecture, chaque arbitrage de roadmap, chaque innovation listée doit servir cette promesse — ou être abandonné.

1.1 Présentation du Projet
RheoSim Enterprise (nom de code RSE, alternative commerciale envisagée : ViscoForge) est une plateforme logicielle scientifique dédiée à la modélisation, la simulation, l'identification paramétrique et la visualisation du comportement visco-élastique des matériaux. Le projet vise à couvrir l'intégralité du cycle scientifique — de la donnée expérimentale brute au rapport de simulation prêt à publication — dans un environnement unifié, reproductible et piloté par les standards ouverts.
Le logiciel s'articule autour d'un cœur physique commun (modèles constitutifs Maxwell, Kelvin-Voigt, Prony) et de moteurs de discrétisation interchangeables (FEM prioritaire, FVM en extension), orchestrés par une architecture microservices moderne. Cette séparation stricte entre physique, numérique et interface constitue la colonne vertébrale du projet.
1.2 Vision Globale
« Passer de l'essai rhéologique isolé à un jumeau numérique matériau vivant, exploitable du laboratoire à la chaîne de production. »
— Vision RheoSim
La vision produit s'articule autour de trois convictions structurantes :
1.	Le fossé recherche-industrie est un problème logiciel. Les laboratoires utilisent du code non-pérenne (scripts Python, fiches Excel), les industriels s'enferment dans des licences coûteuses (ANSYS, Abaqus). Entre les deux : un vide exploitable.
2.	La reproductibilité est une fonctionnalité, pas un sous-produit. Un format case.json bit-exact, un export Dublin Core, une bibliothèque de matériaux versionnée — voilà l'infrastructure invisible qui transforme un outil en standard.
3.	L'intelligence artificielle n'est utile qu'intégrée. Pas un chatbot greffé en façade : une boucle d'active learning qui suggère les prochaines températures à tester, un classifieur qui recommande Prony-5 plutôt que Maxwell-1, un réseau neuronal qui raffine les shift factors TTSP.
1.3 Positionnement
RheoSim Enterprise se positionne comme une plateforme scientifique hybride, à l'intersection de trois segments :
Segment	Attente principale	Livrable RheoSim
Recherche académique	Reproductibilité, flexibilité, export publication	case.json, exports LaTeX/PDF Dublin Core, API Python
Industrie (R&D matériaux)	Fiabilité, validation, traçabilité, intégration CAO	Conformité ASTM/ISO, connecteurs Abaqus/OpenFOAM, audit trail
Enseignement supérieur	Pédagogie, coût, simplicité	Mode éducatif interactif, licences campus, visualisations guidées

Le modèle de distribution retenu est un modèle hybride : cœur open-source (Apache 2.0 recommandé) + modules entreprise propriétaires (IA avancée, SSO, support). Cette stratégie permet d'attirer la communauté scientifique tout en générant un revenu industriel soutenable.
1.4 Proposition de Valeur
La proposition de valeur de RheoSim Enterprise se décline en cinq bénéfices quantifiables, articulés autour d'un gain de productivité mesurable et d'une élévation qualitative du livrable scientifique :
Bénéfice	Métrique cible	Bénéficiaire principal
Réduction du temps de calibrage	De 5-10 jours à < 30 minutes (facteur 200×)	Ingénieur R&D, chercheur
Augmentation de la qualité du fit	R² > 0,98 sur données DMA standards	Scientifique
Reproductibilité totale	100% des runs rejouables à partir du case.json	Revue par les pairs, audit qualité
Intégration chaîne CAO	Export Abaqus .inp, ANSYS .cdb, OpenFOAM	Bureau d'études
Réduction des essais physiques	De 30 à 40% d'expériences en moins grâce à l'active learning	Management R&D (budget)

⚡ Synthèse du Résumé Exécutif
RheoSim Enterprise n'est pas « encore un simulateur de plus ». C'est une plateforme qui réunit trois ruptures simultanées : (1) unification du workflow complet expérience → prédiction, (2) intelligence artificielle native et non postiche, (3) reproductibilité scientifique comme principe fondateur.

Le projet est ambitieux mais circonscrit : il se concentre sur la visco-élasticité linéaire et quasi-linéaire, laissant volontairement hors périmètre la plasticité, la rupture et les grandes déformations — qui feront l'objet d'extensions ultérieures.
 
PARTIE 2 — Problématique
2.1 Le Problème Résolu
Le comportement visco-élastique caractérise une vaste famille de matériaux — polymères, élastomères, bitumes, tissus biologiques, composites à matrice polymère, mousses, gels — dont la réponse mécanique dépend à la fois de l'amplitude de la sollicitation et du temps durant lequel elle est appliquée. Contrairement à l'élasticité linéaire (qui admet un module d'Young scalaire) ou à la plasticité (qui s'exprime par des lois d'écoulement instantanées), la visco-élasticité exige une modélisation temporelle : fluage sous charge constante, relaxation sous déformation imposée, hystérésis sous sollicitation cyclique, et dépendance fréquentielle en régime dynamique.
Aujourd'hui, tout ingénieur ou chercheur qui doit caractériser, puis prédire le comportement d'un tel matériau fait face à une chaîne outillée mais discontinue :
•	Les données expérimentales sortent de la machine DMA ou du rhéomètre au format CSV propriétaire.
•	Le prétraitement (filtrage, lissage, unités) se fait dans Excel ou un script Python ad-hoc.
•	L'identification des paramètres du modèle constitutif (Maxwell, Prony...) se fait dans MATLAB, Origin, ou une feuille de calcul maison.
•	La simulation de la pièce réelle se fait dans Abaqus, ANSYS ou Comsol, avec ré-entrée manuelle des coefficients — source majeure d'erreurs.
•	La comparaison modèle-réalité se fait dans encore un autre outil.
•	Le rapport final compile manuellement figures et tableaux dans Word ou LaTeX.
Cette chaîne est lente, fragile, non-reproductible et induit une perte d'information à chaque transition. RheoSim Enterprise supprime ces frontières en proposant un environnement unifié où chaque étape s'exécute sur les mêmes données sources, dans le même format canonique (case.json + dataset.parquet), avec la même logique d'identification paramétrique.
2.2 Pourquoi C'est Important
Importance scientifique
La visco-élasticité n'est pas un phénomène de second ordre : dans les polymères structuraux (matrices composites époxy, polyamides aéronautiques), les effets visco-élastiques à long terme déterminent directement la durée de vie des pièces. Négliger la relaxation contrainte dans une fixation boulonnée, ou le fluage dans une structure composite sous chargement permanent, conduit à des dimensionnements faux — avec des conséquences potentiellement critiques en aéronautique ou en biomédical (prothèses).
Importance industrielle
Le marché des polymères techniques croît à un rythme soutenu, porté par l'électrification automobile, la transition vers les composites aéronautiques, et le développement de matériaux bio-sourcés. Chaque nouveau grade polymère exige une campagne de caractérisation visco-élastique. Avec 5 à 10 jours d'ingénieur par grade et un coût de 15 000 à 40 000 € de machines (DMA + rhéomètre + logiciels), l'économie réalisable par automatisation est directement mesurable.
Importance pédagogique
La visco-élasticité est enseignée en Master 2 et en école d'ingénieurs, mais la plupart des étudiants ne voient jamais une identification paramétrique réelle : ils manipulent des courbes théoriques sans confrontation à la donnée. Un outil unifié, interactif, avec un mode pédagogique, permettrait de combler ce manque et d'accélérer la montée en compétence des jeunes ingénieurs.
2.3 Limites des Solutions Actuelles
Un audit rigoureux du paysage outil existant met en lumière des lacunes structurelles :
Outil / Famille	Forces	Faiblesses majeures	Positionnement RheoSim
Abaqus / ANSYS (FEA commerciaux)	Solveurs mûrs, écosystème CAO	Licences 20k-50k€/an, identification paramétrique hors logiciel, reproductibilité faible	Complémentaire : export vers ces outils
OpenFOAM	Open-source, FVM robuste	Orienté CFD, visco-élasticité solide marginale, courbe d'apprentissage brutale	Complémentaire : couplage thermique
MATLAB + Simscape	Flexibilité, identification Lévenberg-Marquardt	Licence coûteuse, pas d'architecture de déploiement, scripts non industrialisables	Remplacement partiel
Rheometer / DMA software OEM	Intégré à la machine	Fermé, propriétaire, modèles limités, aucune simulation 3D	Remplacement total
Scripts Python / Jupyter	Gratuit, flexible	Non maintenable, pas de UI, pas de collaboration, pas de standards	Remplacement total

🎯 Le Gap Exploitable
Aucun outil actuel ne couvre simultanément : (1) l'import brut depuis la machine, (2) l'identification paramétrique automatique, (3) la simulation 3D FEM, (4) la visualisation moderne, (5) l'export reproductible au format ouvert. RheoSim Enterprise occupe exactement cet espace vacant.
2.4 Enjeux Scientifiques et Industriels
Enjeux scientifiques
La communauté rhéologique internationale (SoR, GFR, ESR) pointe trois défis ouverts qu'un outil moderne devrait adresser :
•	L'identification non-unique : pour un jeu de données donné, plusieurs jeux de paramètres Prony peuvent fitter avec un R² équivalent. Il faut une méthodologie de régularisation robuste (Tikhonov, contraintes physiques) pour converger vers des paramètres physiquement interprétables.
•	La propagation d'incertitude : les paramètres identifiés ont une incertitude qu'il faut propager dans la simulation, via analyse de sensibilité (Sobol) ou bootstrap.
•	La fidélité prédictive hors domaine : un modèle calibré à 25°C prédit-il correctement à -40°C ? La méthode TTSP existe mais est rarement automatisée rigoureusement.
Enjeux industriels
Côté industrie, les défis sont davantage organisationnels et économiques :
•	Le time-to-characterization : réduire le délai entre la réception d'un nouveau matériau et sa mise à disposition dans la chaîne simulation. Objectif : passer de semaines à jours.
•	La traçabilité qualité : dans les secteurs réglementés (aéronautique EN 9100, biomédical ISO 13485), chaque simulation doit être auditable. Un case.json signé numériquement et archivé dans un object storage WORM répond à cette exigence.
•	L'indépendance technologique : dépendre d'un seul éditeur de solveur (ANSYS par exemple) constitue un risque stratégique pour un grand industriel. Une alternative open-core comme RheoSim offre une option de repli.
 
PARTIE 3 — Vision Produit
3.1 Description du Logiciel
RheoSim Enterprise est une application web progressive (PWA) à architecture distribuée, accessible depuis un navigateur moderne, qui orchestre une pile de microservices backend et un moteur de calcul haute performance en C++. L'interface utilisateur privilégie la fluidité et l'exploration interactive : l'utilisateur importe ses données, bascule entre modèles, lance des identifications, visualise les résultats, annote ses observations, et exporte son travail — tout cela sans jamais quitter le navigateur.
Le logiciel se présente comme un espace de travail organisé autour de la notion de projet. Un projet contient un ou plusieurs matériaux, chacun associé à des campagnes expérimentales, des modèles calibrés, des simulations 3D, et des rapports. L'arborescence projet/matériau/campagne/simulation/rapport est l'unité cognitive fondamentale : elle reflète la pratique réelle des ingénieurs de recherche.
Principales capacités fonctionnelles
•	Import multi-format : CSV, Excel, formats rhéomètre natifs (Anton Paar, TA Instruments, Malvern), ainsi qu'une API d'upload pour intégration en laboratoire automatisé.
•	Bibliothèque de matériaux : base de données versionnée (PostgreSQL + git-like) pré-peuplée avec 50 à 100 matériaux standards (PA6, PC, EPDM, PEEK, etc.) issus de la littérature et des datasets ouverts NIST.
•	Identification paramétrique : algorithmes L-BFGS-B, Levenberg-Marquardt, NLopt avec contraintes physiques (positivité, ordonnancement des τᵢ), assistance IA pour suggestion du nombre de branches Prony.
•	Simulation 3D FEM : maillages importés (Gmsh, Abaqus), conditions aux limites Dirichlet / Neumann / mixtes, intégration temporelle Newmark ou generalized-α, champs σ et ε exportables en VTK/VTU.
•	Visualisation scientifique : courbes 2D interactives (Chart.js / D3), champs 3D animés (VTK.js + WebGL), diagrammes Cole-Cole, master curves TTSP, résidus.
•	Comparaison & métriques : RMSE, MAE, R², erreur maximale, tests de normalité des résidus (Shapiro-Wilk) pour détecter les biais systématiques.
•	Export & reporting : rapports PDF avec métadonnées Dublin Core, snippets LaTeX prêts à coller, CSV/JSON, VTK/VTU, et format natif case.json.
3.2 Utilisateurs Cibles
Trois personae structurent la conception produit. Chaque decision UX doit être évaluée à l'aune de ces trois profils.
Persona 1 — Élise, ingénieure R&D matériaux (32 ans)
Profil
Contexte : équipementier automobile, département polymères, 8 ans d'expérience.
Outils actuels : Excel, Abaqus, script MATLAB hérité de son prédécesseur.
Objectif : caractériser un nouveau grade EPDM en 3 jours au lieu de 2 semaines.
Frustration : perdre des heures à reformater des données entre outils.
Attente RheoSim : un workflow qui assume que le temps ingénieur est précieux.

Persona 2 — Dr. Moreau, chercheur académique (47 ans)
Profil
Contexte : laboratoire universitaire, encadrement de doctorants, publications ESR Journal of Rheology.
Outils actuels : Python (numpy, scipy), Origin, LaTeX.
Objectif : explorer de nouveaux modèles constitutifs, publier des résultats reproductibles.
Frustration : ses doctorants passent 40% de leur thèse à coder leur propre solveur.
Attente RheoSim : un socle robuste avec API Python pour leurs extensions, et exports LaTeX.

Persona 3 — Kenji, étudiant Master 2 (24 ans)
Profil
Contexte : stage industriel 6 mois dans un bureau d'études.
Outils actuels : formations variables selon le cours, Excel/Python.
Objectif : comprendre ce qu'il manipule, produire un livrable propre.
Frustration : outils trop complexes ou trop magiques.
Attente RheoSim : un mode pédagogique qui explique les étapes, affiche les équations, décompose les calculs.
3.3 Cas d'Usage Concrets
Cas d'usage 1 — Caractérisation rapide d'un grade polymère (industrie)
Élise reçoit 500 mg d'un nouveau polyamide de son fournisseur. Elle effectue trois essais DMA à 25°C, 60°C, 100°C dans la matinée. À 14h, elle importe les trois fichiers CSV dans RheoSim. Le système détecte automatiquement le format (Anton Paar), propose une série de Prony à 5 branches (recommandation ML), lance l'identification TTSP avec shift factor WLF automatique. À 14h30, elle a une master curve, un jeu de paramètres identifié, et un rapport PDF prêt pour son superviseur.
Cas d'usage 2 — Exploration d'un nouveau modèle (recherche)
Le Dr. Moreau souhaite tester un modèle fractionnaire (Scott-Blair) qu'il vient de publier. Il connecte son plugin Python (SDK RheoSim) qui expose son modèle comme une ConstitutiveLaw. Il l'ajoute au catalogue de son équipe, ses trois doctorants peuvent immédiatement le confronter à leurs données. Les résultats sont versionnés avec le numéro de commit Git du plugin, garantissant la reproductibilité.
Cas d'usage 3 — Pédagogie en cours de Master (enseignement)
Kenji suit un cours sur la visco-élasticité. Le professeur partage un projet RheoSim contenant 10 matériaux types et 5 expériences guidées. Kenji active le mode pédagogique : à chaque étape, une bulle explicative affiche l'équation manipulée, son interprétation physique, et le calcul numérique intermédiaire. À la fin du semestre, il a produit un portfolio de simulations reproductibles qu'il peut joindre à sa candidature de stage.
Cas d'usage 4 — Validation d'un composant aéronautique (ingénierie)
Une équipe bureau d'études doit valider la durée de vie en fluage d'un joint EPDM dans un actionneur. Ils chargent le maillage 3D Abaqus du joint, importent les paramètres matériaux identifiés, lancent la simulation de fluage sur 10 ans (avec accélération TTSP). Le résultat est un champ de déformation visualisable à tout instant, et un rapport d'audit signé numériquement, conforme EN 9100.
3.4 Expérience Utilisateur — Workflow Complet
Le workflow utilisateur canonique — optimisé pour la persona industrielle mais accessible aux deux autres — se décompose en huit étapes explicites. Chacune est associée à un temps cible qui guide les arbitrages d'implémentation.
Étape	Action utilisateur	Action système	Temps cible
1	Créer un projet + choisir un matériau (nouveau ou bibliothèque)	Initialiser le case.json, proposer un template	< 30 sec
2	Importer les données expérimentales (drag & drop)	Auto-détection du format, validation du schéma, aperçu graphique	< 10 sec
3	Choisir le protocole d'essai (fluage, relaxation, DMA, TTSP...)	Configurer automatiquement le solveur correspondant	< 15 sec
4	Sélectionner un modèle constitutif (ou accepter la recommandation ML)	Afficher les équations, proposer valeurs initiales	< 20 sec
5	Lancer l'identification paramétrique	Optimisation L-BFGS-B, feedback de progression, affichage des résidus	10 sec à 5 min
6	Analyser les résultats, affiner, itérer	Graphiques interactifs, métriques, assistant d'analyse	Variable
7	[Optionnel] Lancer une simulation 3D d'une pièce	Soumettre le job au compute engine, notifier à la fin	1 à 30 min
8	Générer le rapport et exporter	PDF Dublin Core + VTK + case.json + snippet LaTeX	< 15 sec

🧭 Principes UX fondamentaux
① Optimistic UI — l'interface répond instantanément, les calculs longs tournent en arrière-plan avec notifications.
② Keyboard-first — raccourcis clavier pour toutes les actions fréquentes, mode command palette (Ctrl+K).
③ Exploratoire — chaque action est annulable (Ctrl+Z profond jusqu'à 100 étapes), aucune destruction irréversible.
④ Transparent — chaque chiffre affiché est cliquable pour voir son origine (équation, donnée, calcul).
⑤ Exportable — rien n'est enfermé : tout ce qui est affiché est téléchargeable dans un format ouvert.
 
3.5 UX Concrète — Description des Écrans Principaux
Cinq écrans portent l'essentiel de l'expérience utilisateur. Ils sont décrits ci-dessous en termes de layout, composants, interactions et données affichées. Ces descriptions servent de brief direct pour le designer UI et le développeur frontend.
Écran 1 — Upload & Validation du Dataset Expérimental
Objectif : permettre à l'utilisateur d'importer ses données rhéomètre / DMA en moins de 30 secondes, avec validation immédiate.
┌──────────────────────────────────────────────────────────────────────┐
│  ◀ Projet PA6-GradeA / Données expérimentales            ✕ Fermer  │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│   ┌──────────────────────────┐   ┌────────────────────────────────┐  │
│   │                          │   │  📋 Formats détectés           │  │
│   │   Glissez-déposez ici    │   │  • Anton Paar (.rpf)           │  │
│   │       OU CLIQUEZ         │   │  • TA Instruments (.tri)       │  │
│   │     pour parcourir       │   │  • Malvern (.msn)              │  │
│   │                          │   │  • CSV générique               │  │
│   │   .csv .xlsx .rpf .tri   │   │  • Excel multi-feuilles        │  │
│   │                          │   └────────────────────────────────┘  │
│   └──────────────────────────┘                                       │
│                                                                      │
│   ─────────  ou import via API  ─────────                            │
│                                                                      │
│   📜 Fichiers récents du projet                                      │
│   ▸ relax_25C.csv          12 ko    2 mn  [↻] [👁] [⤓]             │
│   ▸ DMA_sweep_60C.tri      48 ko    1 h   [↻] [👁] [⤓]             │
│                                                                      │
├──────────────────────────────────────────────────────────────────────┤
│              [ Annuler ]              [ Valider et continuer → ]     │
└──────────────────────────────────────────────────────────────────────┘
Composants & interactions
•	Zone de drop principale : large, hint visuel clair, gère drag-multiple.
•	Détection automatique du format (header sniffing + signatures binaires) ; en cas d'ambiguïté, modal de mapping colonnes.
•	Aperçu graphique immédiat (chart courbe brute) avant validation finale — laisse l'utilisateur détecter une anomalie en 2 secondes.
•	Validation Background : schéma JSON, unités, monotonicité du temps, doublons → liste d'avertissements non-bloquants.
•	Historique des fichiers du projet, avec actions rapides (revisualiser, télécharger, archiver).

Écran 2 — Calibration du Modèle (Identification Paramétrique)
Objectif : identifier les paramètres du modèle constitutif en montrant en temps réel la convergence et les résidus.
┌──────────────────────────────────────────────────────────────────────┐
│  Calibration  •  PA6-GradeA  •  Modèle: Prony-5     [Auto-Fit IA] ▶ │
├──────────────────────┬───────────────────────────────────────────────┤
│ MODÈLE & PARAMÈTRES  │   📈 Données vs Modèle (live)                 │
│                      │                                                │
│ Type   ▼ Prony-5     │      ┌──────────────────────────────────┐     │
│ E∞      2.10e9   🔒  │   E  │  ●●●●  données expérimentales    │     │
│ E1      1.30e9       │ (Pa) │   ──   modèle Prony-5           │     │
│ τ1      1.0      s   │      │                                  │     │
│ E2      0.80e9       │      │      ●● ● ● ● ●                  │     │
│ τ2      10.0     s   │      │  ───────────●───●───●───●──     │     │
│ E3      0.50e9       │      │                                  │     │
│ τ3      100.0    s   │      └──────────────────────────────────┘     │
│ ...                  │                  log t (s)                    │
│                      │                                                │
│ ✦ Recommandé par IA  │   📉 Résidus                                  │
│   Prony-5 confiance  │      ┌──────────────────────────────────┐     │
│   92% — pourquoi ?   │      │  •  • • •  •  •   •  •           │     │
│                      │      │ ─────────────────────────────────│     │
│ [⚙ Régul. avancée]   │      │     • • •     •         •  •     │     │
│                      │      └──────────────────────────────────┘     │
│                      │                                                │
│                      │   Métriques :  R² = 0.9981   RMSE = 1.4e7    │
├──────────────────────┴───────────────────────────────────────────────┤
│  Itération 7/50  ▰▰▰▰▰▱▱▱▱▱  [⏸ Pause]  [✓ Accepter]  [↺ Reset]   │
└──────────────────────────────────────────────────────────────────────┘
Composants & interactions
•	Panneau gauche : table de paramètres éditable, cadenas pour fixer un paramètre, suggestions IA cliquables.
•	Bouton Auto-Fit IA en haut à droite — un clic, l'optimiseur démarre, l'utilisateur voit la convergence en direct.
•	Graphiques live : la courbe modèle s'actualise à chaque itération, le panneau résidus aussi.
•	Métriques R² / RMSE / MAE en temps réel, code couleur (vert > 0.99, orange 0.95-0.99, rouge < 0.95).
•	Tooltip « pourquoi cette recommandation ? » → SHAP values du Model Recommender (transparence IA).
•	Boutons Pause / Accepter / Reset toujours visibles — l'utilisateur garde le contrôle.

Écran 3 — Visualisation 3D des Champs Simulés
Objectif : explorer les champs σ et ε en 3D sur le maillage, animer dans le temps, extraire des sondes.
┌──────────────────────────────────────────────────────────────────────┐
│  ◀ Simulation #4271 — Joint EPDM fluage 10 ans       [⤓ Export VTK] │
├──────────────────┬───────────────────────────────────────┬───────────┤
│ FIELDS           │                                       │ TIME      │
│                  │                                       │           │
│ ◉ σ_vonMises     │           [VIEWPORT 3D WebGL]         │  t = 4.2y │
│ ○ σ_xx σ_yy σ_zz │                                       │           │
│ ○ ε_vonMises     │              ╔══════╗                 │  ▶ ▮ ◀ ▶▶│
│ ○ ε_p (plast.)   │             ╔╝      ╚╗                │  ━━━━●━━━│
│ ○ Internal q_i   │            ╔╝   ●    ╚╗               │  0      10y│
│                  │           ╔╝            ╚╗             │           │
│ COLORMAP         │          ╚════════════════╝            │ SNAPSHOTS │
│ ▣▣▣▣▣▣▣ Viridis │     ↑           ↑                       │  ◾ t=0    │
│ Min  0.0  MPa    │   sonde A    sonde B                  │  ◾ t=1y   │
│ Max  35.2 MPa    │                                       │  ◾ t=4y ◀ │
│                  │                                       │  ◾ t=10y  │
│ DISPLAY          │                                       │           │
│ ☑ Mesh edges     │                                       │ PROBES    │
│ ☑ Colorbar       │   [🔄 reset view] [📐 measure] [📷]   │ A: 22 MPa │
│ ☐ Deformed (×100)│                                       │ B: 18 MPa │
│ ☐ Vector field   │                                       │ [+ probe] │
└──────────────────┴───────────────────────────────────────┴───────────┘
Composants & interactions
•	Viewport central plein écran : VTK.js + WebGL, contrôles caméra orbit/pan/zoom, sélection de sonde au clic.
•	Panneau gauche FIELDS : choix du champ scalaire/vectoriel/tensoriel, colormap éditable, bornes auto ou manuelles.
•	Panneau droite TIME : timeline interactive (drag pour scrubbing), contrôles de lecture, snapshots pré-calculés en miniatures.
•	Panneau droite PROBES : sondes ajoutées par clic dans le viewport, valeur live + courbe temporelle disponible en popover.
•	Toolbar viewport : reset view, mesure de distance, capture PNG, export image animée (GIF / MP4 court).
•	Performance : level-of-detail automatique sur gros maillages (sous-échantillonnage à la rotation, full mesh à l'arrêt).

Écran 4 — Comparaison Modèle vs Réalité
Objectif : permettre à l'utilisateur de juger en quelques secondes si son modèle est acceptable, et où il diverge.
┌──────────────────────────────────────────────────────────────────────┐
│  Comparaison  •  PA6-GradeA  •  3 jeux de données  •  Modèle Prony-5│
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│   📊 Vue superposée                                                  │
│   ┌────────────────────────────────────────────────────────────┐     │
│   │                                                            │     │
│   │  E(t)  ●  Run #1 25°C       — Modèle Prony-5 ajusté       │     │
│   │       ▲  Run #2 60°C        ┄┄ Modèle TTSP shifted        │     │
│   │       ■  Run #3 100°C                                     │     │
│   │                                                            │     │
│   │     log E                                                  │     │
│   │      ▲                                                     │     │
│   │      │   ●●●─────                                          │     │
│   │      │   ▲▲▲────────                                       │     │
│   │      │   ■■■─────────────                                  │     │
│   │      └──────────────────────▶ log t                       │     │
│   └────────────────────────────────────────────────────────────┘     │
│                                                                      │
│   📋 Tableau métriques                                               │
│   ┌──────────┬─────────┬────────────┬──────────┬────────────┐       │
│   │ Dataset  │   R²    │ RMSE (MPa) │ MAE      │ Status     │       │
│   ├──────────┼─────────┼────────────┼──────────┼────────────┤       │
│   │ Run #1   │ 0.9981  │   0.014    │  0.011   │ ✓ Excellent│       │
│   │ Run #2   │ 0.9942  │   0.022    │  0.018   │ ✓ Bon      │       │
│   │ Run #3   │ 0.9603  │   0.087    │  0.061   │ ⚠ Moyen    │       │
│   └──────────┴─────────┴────────────┴──────────┴────────────┘       │
│                                                                      │
│   💡 Assistant : « Run #3 (100°C) montre une dérive systématique     │
│      en zone log t > 2. Suggestion : ajouter une 6e branche Prony   │
│      ou explorer un modèle fractionnaire. »                         │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
Composants & interactions
•	Vue superposée : multi-courbes data + modèle, légende riche, toggle individuel par dataset, log/lin axes.
•	Tableau de métriques : R², RMSE, MAE, erreur max, status code couleur, tri par colonne, export CSV.
•	Encart Assistant IA : analyse textuelle automatique des résidus, formulée en langage naturel actionnable.
•	Vue toggleable : superposée / résidus / parité (data vs modèle, ligne y=x) / Cole-Cole pour DMA.
•	Action « Re-fit avec suggestion » qui applique la suggestion de l'assistant en un clic.

Écran 5 — Génération du Rapport Scientifique
Objectif : produire en moins de 15 secondes un livrable PDF prêt à diffuser, avec personnalisation contrôlée.
┌──────────────────────────────────────────────────────────────────────┐
│  Génération de rapport  •  PA6-GradeA           [⏎ Générer PDF]     │
├────────────────────────────────┬─────────────────────────────────────┤
│ TEMPLATE                       │                                     │
│                                │      📄 Aperçu du rapport          │
│ ◉ Rapport ingénieur (12p)      │                                     │
│ ○ Rapport exécutif (2p)        │     ┌─────────────────────────┐     │
│ ○ Article scientifique LaTeX   │     │  Caractérisation visco- │     │
│ ○ Dossier qualité ASTM D2990  │     │  élastique du PA6 GradeA│     │
│                                │     │                         │     │
│ SECTIONS À INCLURE             │     │  E. Durand, ACME R&D    │     │
│ ☑ Résumé                       │     │  15 avril 2026          │     │
│ ☑ Méthodologie                 │     │                         │     │
│ ☑ Données expérimentales       │     │  ━━━━━━━━━━━━━━━━━━━━ │     │
│ ☑ Modèle identifié             │     │                         │     │
│ ☑ Validation & métriques       │     │  1. Résumé              │     │
│ ☑ Figures (8 sélectionnées)    │     │     Le PA6 GradeA a été │     │
│ ☑ Annexe : case.json complet   │     │     caractérisé en      │     │
│ ☐ Code Python reproductible    │     │     fluage et DMA...    │     │
│ ☑ Bibliographie automatique    │     │                         │     │
│                                │     │  [page 1 / 12]          │     │
│ MÉTADONNÉES Dublin Core        │     └─────────────────────────┘     │
│ Auteur : Élise Durand          │                                     │
│ Affil. : ACME R&D              │     ◀ page  ▶                       │
│ DOI    : [auto-générer]        │                                     │
│ Licence : CC-BY 4.0     ▼      │                                     │
│                                │                                     │
│ EXPORTS COMPLÉMENTAIRES        │                                     │
│ ☑ PDF        ☑ case.json       │                                     │
│ ☑ VTK 3D     ☑ snippets LaTeX  │                                     │
│ ☐ Abaqus .inp ☐ ANSYS .cdb    │                                     │
└────────────────────────────────┴─────────────────────────────────────┘
Composants & interactions
•	Choix de template à gauche : 4 templates pré-conçus + custom ; les sections suivantes s'adaptent automatiquement.
•	Checkboxes de sections : preview se met à jour en quasi-temps-réel (< 500ms).
•	Métadonnées Dublin Core : pré-remplies avec le profil utilisateur, auto-DOI si activé (Crossref API en V3).
•	Aperçu PDF dans iframe paginée à droite, navigation page-à-page.
•	Exports complémentaires : zip téléchargeable contenant le PDF + tous les artefacts cochés.
•	Bouton Générer PDF avec compteur de pages et estimation de taille avant l'action.

🎨 Principes UX transverses aux 5 écrans
① Densité d'information maîtrisée : chaque écran sert un objectif unique, pas de fonctionnalités secondaires en mode brouillon.
② Action principale toujours visible : un seul bouton primaire par écran (Valider / Auto-Fit / Export / Re-fit / Générer).
③ Feedback immédiat : tout calcul long affiche progression + ETA + bouton Annuler. Aucune action ne reste silencieuse plus de 2 secondes.
④ Réversibilité : Ctrl+Z fonctionne sur la dernière modification de paramètre, Ctrl+Shift+Z restaure. Pas de boîte de dialogue « êtes-vous sûr ? » sauf pour suppression définitive.
⑤ Cohérence visuelle : palette unique (bleu profond #1A4D7A), grille 8px, composants réutilisés (boutons, tables, charts). Pas de divergence entre écrans.
PARTIE 4 — Différenciation & Innovation
4.1 Méthode d'Évaluation
Toute proposition d'amélioration est évaluée ici selon trois critères stricts, afin de distinguer les vraies innovations (valeur durable, défendable) des gadgets (effet waouh de courte durée, coût de maintenance élevé pour bénéfice marginal).
Critère	Description
Valeur réelle	L'amélioration résout-elle un problème utilisateur douloureux, ou s'agit-il d'une astuce marketing ? Mesurable par entretiens utilisateurs et A/B tests.
Défendabilité	L'amélioration crée-t-elle une barrière à l'entrée (moat) ? Données propriétaires, algorithme entraîné, effet de réseau, sinon compétiteur peut copier en 3 mois.
Coût / bénéfice	Effort d'implémentation vs gain utilisateur. Une fonctionnalité à 6 mois de dev pour 5% d'utilisateurs est généralement un piège.

4.2 Vraies Innovations (à implémenter)
Innovation 1 — Calibration automatique intelligente (Auto-Fit IA)
L'identification paramétrique manuelle est le point de douleur n°1 des utilisateurs actuels. Le Auto-Fit IA combine trois mécaniques qui, ensemble, constituent une différenciation défendable :
•	Initialisation intelligente : un classifieur ML (Gradient Boosting entraîné sur ~2000 campagnes open-source) prédit un point de départ dans l'espace des paramètres Prony en fonction de la signature spectrale de la donnée. Gain : passe de ~50 itérations L-BFGS-B en moyenne à ~8 itérations.
•	Régularisation adaptative : Tikhonov sur la norme log(τᵢ) pour éviter les τ dégénérés, avec choix automatique du paramètre de régularisation par L-curve.
•	Contraintes physiques intégrées : positivité stricte des modules Eᵢ, hiérarchie τ₁ < τ₂ < ... < τₙ, plages admissibles par famille matériau (polymère vitreux vs caoutchouc).
Ce pipeline rend l'identification à la fois plus rapide, plus stable (convergence fiable même sur données bruitées), et plus interprétable physiquement. Défendabilité : dataset propriétaire construit sur 18 mois, difficile à reconstituer par un compétiteur.
Innovation 2 — Model Recommender (recommandation du meilleur modèle)
Quel modèle choisir entre Maxwell, Kelvin-Voigt, Prony-3, Prony-5, Burgers, fractionnaire ? Cette décision se prend aujourd'hui par expertise tacite. RheoSim la rend explicite et reproductible :
•	Input : signature de la donnée (type d'essai, plage fréquentielle/temporelle, forme de la courbe) + métadonnées matériau (famille, Tg approximative si connue).
•	Output : un ranking de 5 modèles avec probabilité de bonne adéquation + explication (SHAP values sur les features).
•	Pédagogie intégrée : l'utilisateur voit POURQUOI Prony-4 est recommandé (présence de deux temps caractéristiques bien séparés détectés dans le spectre).
Innovation 3 — Active Learning pour la planification expérimentale
Quand on caractérise un nouveau matériau, on ne sait pas a priori quelles températures, quelles fréquences, quels niveaux de contrainte tester. L'active learning résout ce problème en boucle fermée :
4.	L'utilisateur fournit 2-3 expériences initiales.
5.	Le système identifie un modèle provisoire avec son incertitude paramétrique (bootstrap ou analyse bayésienne).
6.	Le système suggère la prochaine expérience qui réduirait le plus l'incertitude (Maximum Information Gain, critère D-optimal).
7.	L'utilisateur réalise l'essai, ré-entre dans la boucle.
Résultat typique : réduire de 30-40% le nombre d'essais physiques nécessaires pour atteindre une incertitude paramétrique cible. Pour un laboratoire qui paie 200 à 500 € l'heure de DMA, l'économie est directe.
Innovation 4 — Bibliothèque de matériaux versionnée & collaborative
Inspirée des registres de packages (npm, PyPI), la bibliothèque de matériaux est un catalogue versionné où chaque matériau a une histoire : qui a contribué, sur quelles données, avec quel modèle, à quelle date. Chaque entrée a un DOI citable. Deux niveaux :
•	Catalogue public : matériaux ouverts (NIST, publications), peer-reviewed par la communauté, citables dans les articles.
•	Catalogue privé entreprise : matériaux internes avec contrôle d'accès, export vers Abaqus/ANSYS, synchronisation multi-sites.
C'est un effet de réseau puissant : plus il y a de matériaux, plus l'outil devient incontournable, et plus les utilisateurs contribuent. Défendabilité maximale à moyen terme.
Innovation 5 — Reproductibilité by Design (case.json signé)
Chaque simulation produit un case.json auto-suffisant — modèle, paramètres, conditions, version des solveurs — signé cryptographiquement. Relancer ce fichier sur n'importe quelle instance de RheoSim doit produire un résultat bit-exact (ou à epsilon près pour les opérations non-déterministes, clairement documentées). Cette reproductibilité bit-exact est rarement atteinte dans la simulation scientifique actuelle.
Applications : revue par les pairs accélérée, audit qualité industriel (EN 9100, ISO 13485), reproduction de résultats publiés en un clic.
Innovation 6 — Assistant d'analyse des résultats (IA explicative)
Après l'identification ou la simulation, un assistant textuel (basé sur un LLM spécialisé, local ou cloud selon la configuration entreprise) lit automatiquement les résultats et produit un paragraphe d'analyse en langage naturel : détection d'anomalies, comparaison avec la littérature, suggestions d'investigation complémentaire. Cet assistant N'EST PAS une fenêtre de chat libre — il produit des annotations structurées validables.
Exemple : « Le résidu présente une structure oscillatoire à ~1Hz non expliquée par le modèle Prony-3. Cela suggère un mécanisme relaxation secondaire. Modèle Prony-5 ou fractionnaire recommandé. »
Innovation 7 — Mode pédagogique interactif
Un toggle dans l'interface active un mode pédagogique destiné à l'enseignement et aux onboarding ingénieurs juniors. Dans ce mode :
•	Chaque équation manipulée est affichée à côté du résultat numérique.
•	Des annotations guidées pointent « ici, le module de relaxation décroît exponentiellement, voyez comment τ₁ gouverne cette échelle ».
•	Des exercices prédéfinis (« identifier les paramètres de ce dataset ») permettent l'auto-apprentissage.
•	Des scénarios guidés reproduisent des expériences historiques (expérience de Tobolsky 1943, etc.).
Valeur business : ouverture du marché enseignement (universités), création d'une communauté d'utilisateurs formés dès leur cursus — qui deviendront les ingénieurs prescripteurs dans 3-5 ans.
Innovation 8 — Workflows de validation expérimentale
Chaque expérience standard (ASTM D4065, ISO 6721, ASTM D2990 fluage) est packagée comme un workflow exécutable. L'ingénieur choisit la norme visée, le système génère automatiquement la checklist de conformité, vérifie que les paramètres d'essai respectent les tolérances, et produit un rapport conforme directement utilisable dans un dossier qualité. C'est le genre de fonctionnalité apparemment banale mais critique pour l'adoption industrielle.
Innovation 9 — Génération automatique de rapports scientifiques
Trois niveaux de livrables, sélectionnables par l'utilisateur :
•	Rapport exécutif (2 pages) : pour décideur non-technique, résumé chiffré, figures choisies, conclusion actionnable.
•	Rapport ingénieur (10-15 pages) : méthodologie, paramètres identifiés avec incertitudes, figures complètes, références.
•	Rapport scientifique (article ready) : sections pré-remplies au format LaTeX (Elsevier, Springer), bibliographie insérée, snippets de code Python pour reproduction.
4.3 Idées Gadgets (à ne PAS implémenter)
Par honnêteté intellectuelle, voici des idées qui semblent attractives mais qui, évaluées contre les trois critères, sont des pièges :
Idée	Pourquoi elle semble attractive	Pourquoi c'est un piège
Chatbot IA conversationnel	Effet waouh, tendance marché	Coût d'entraînement élevé, hallucinations dangereuses en contexte scientifique, maintenance lourde, pas de moat
Réalité virtuelle / AR	Démo spectaculaire	Adoption marginale (<2% des ingénieurs ont casque au bureau), ROI négatif, coût de dev élevé
Blockchain pour traçabilité	Buzzword attractif	Un simple hash + signature numérique suffit, blockchain ajoute complexité sans valeur ajoutée ici
Génération de modèles par GAN	Différenciation IA forte	Pas assez de données d'entraînement en visco-élasticité, risque de modèles physiquement aberrants, peu défendable
Interface gamifiée (badges, points)	Rétention utilisateur	Audience professionnelle, contre-productif, paraît peu sérieux

⚠️ Discipline d'exécution
La capacité à dire NON à une idée séduisante est une compétence critique en product management. Chaque heure-homme consommée sur une fonctionnalité gadget est une heure volée aux fonctionnalités qui créent une vraie valeur défendable.
 
PARTIE 5 — Architecture Conceptuelle
5.1 Vue Globale du Système
L'architecture de RheoSim Enterprise suit le pattern Hexagonal (Ports & Adapters) au niveau de chaque service, combiné à une décomposition microservices au niveau système. Ce double choix structure le code de manière à ce que les règles métier (physique, algorithmes d'identification, intégration temporelle) restent isolées de l'infrastructure (bases de données, files de messages, frameworks HTTP).
Le système se décompose en quatre grandes couches, empilées de l'utilisateur au matériel :
┌─────────────────────────────────────────────────────────────────────┐
│  COUCHE 1 — PRÉSENTATION                                            │
│  Angular 17 PWA  •  VTK.js WebGL  •  Chart.js  •  NgRx state        │
└─────────────────────────────────────────────────────────────────────┘
                               │  HTTPS / WSS
                               ▼
┌─────────────────────────────────────────────────────────────────────┐
│  COUCHE 2 — API & ORCHESTRATION  (Spring Boot 3 / Java 21)          │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐   │
│  │ Project  │ │ Material │ │   Data   │ │   Job    │ │  Report  │   │
│  │ Service  │ │ Service  │ │ Service  │ │ Service  │ │ Service  │   │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────┘   │
│       Spring Security + Keycloak OAuth2 • OpenAPI 3.0 • Resilience4j│
└─────────────────────────────────────────────────────────────────────┘
                               │  gRPC + RabbitMQ
                               ▼
┌─────────────────────────────────────────────────────────────────────┐
│  COUCHE 3 — COMPUTE ENGINE  (C++20 natif)                           │
│  Physics Core  →  FEM Engine / FVM Engine  →  Linear Solvers        │
│  Eigen • NLopt • PETSc (option) • OpenMP • MPI (phase 2)            │
└─────────────────────────────────────────────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────────────┐
│  COUCHE 4 — STOCKAGE & INFRASTRUCTURE                               │
│  PostgreSQL 15 + TimescaleDB  •  Redis  •  MinIO/S3  •  Keycloak    │
│  Kubernetes  •  Prometheus + Grafana  •  Loki  •  GitLab CI/CD      │
└─────────────────────────────────────────────────────────────────────┘
5.2 Description des Modules
Module UI (Frontend)
Angular 17 avec composants standalone et signals, architecture feature-based. VTK.js pour le rendu 3D (wrapping de VTK dans le navigateur via WebGL / WebGPU en phase 2). Chart.js et D3 pour les visualisations 2D interactives. NgRx comme store d'état global pour la gestion des projets ouverts, notifications, et jobs en cours.
Le frontend est intentionnellement « dumb » : il affiche et capture, mais ne contient aucune logique métier physique. Cette règle garantit que le raisonnement scientifique reste concentré dans le backend, où il est testable, versionné et audité.
Module API (Backend Spring Boot)
Cinq microservices, chacun autour d'un bounded context clair :
Service	Responsabilité	Données propres	Dépendances
Project Service	Projets, utilisateurs, équipes, permissions	projects, teams, users, roles	Material, Job
Material Service	Matériaux, modèles constitutifs, bibliothèque	materials, models, parameters, versions	Project
Data Service	Import/validation des données expérimentales	experiments, datasets, metadata	Material
Job Service	Soumission et suivi des simulations	jobs, runs, status, logs	Compute Engine
Report Service	Génération PDF, LaTeX, exports	reports, templates, exports	Tous

Chaque service expose une API REST documentée OpenAPI 3.0 et un canal gRPC pour les communications inter-services haute fréquence. L'authentification est déléguée à Keycloak (OAuth2 / OIDC), avec support MFA et SSO SAML pour les déploiements entreprise.
Module Compute Engine (C++ haute performance)
Le compute engine est l'atout scientifique de RheoSim. Il est volontairement en C++20 pour trois raisons : (1) performance brute nécessaire aux simulations 3D, (2) compatibilité avec l'écosystème scientifique existant (PETSc, Eigen, Trilinos), (3) absence de garbage collector lors des boucles d'intégration temporelle critiques.
Architecture interne du compute engine :
•	Physics Core : interfaces abstraites ConstitutiveLaw, TimeIntegrator, BoundaryCondition. Implémentations pures, sans dépendance à un solveur.
•	FEM Engine : maillage (via MFEM ou implementation propriétaire légère), assemblage K, M, C ; intégration Gauss ; Newton-Raphson pour les non-linéarités.
•	FVM Engine (phase 2) : maillage polyédrique, schémas centré / upwind, applicable d'abord à la thermique, puis couplage thermo-visco-élastique.
•	Linear Solvers : CG / GMRES via Eigen en MVP, branchement PETSc en phase 2 pour les gros problèmes (> 10⁶ DOFs) avec préconditionneurs AMG.
Module Storage
Trois systèmes de stockage, chacun spécialisé :
•	PostgreSQL 15 : données relationnelles (utilisateurs, projets, métadonnées), schéma normalisé. Extension TimescaleDB pour les séries temporelles expérimentales (buckets temporels, compression).
•	Redis : cache de session, file d'attente légère pour WebSocket, résultats intermédiaires éphémères.
•	MinIO / S3 : stockage objet pour les gros artefacts (maillages, résultats VTK, rapports PDF, exports). Versioning natif, pas de compression automatique pour permettre la reproductibilité bit-exact.
5.3 Flux de Données — Lifecycle d'une Simulation
Le diagramme suivant retrace le chemin complet d'une simulation, de la soumission à l'affichage du résultat, avec les points de contrôle et de persistance :
(1) UTILISATEUR            (2) FRONTEND            (3) API
    │                          │                       │
    │  Submit simulation       │                       │
    ├─────────────────────────▶│                       │
    │                          │  POST /api/jobs       │
    │                          ├──────────────────────▶│
    │                          │                       │ Validate case.json
    │                          │                       │ Persist in PostgreSQL
    │                          │                       │ Upload mesh to MinIO
    │                          │                       │ Publish to RabbitMQ
    │                          │  201 Created          │
    │                          │◀──────────────────────┤
    │                          │                       │
    │                          │                       ▼ (4) RABBITMQ
    │                          │                       │
    │                          │                       ▼ (5) COMPUTE ENGINE
    │                          │                       │  Fetch case + mesh
    │                          │                       │  Run FEM simulation
    │                          │                       │  Store results in MinIO
    │                          │                       │
    │                          │  WebSocket progress   │  Publish status events
    │                          │◀──────────────────────┤
    │  Progress bar updates    │                       │
    │◀─────────────────────────┤                       │
    │                          │                       │
    │                          │  GET /api/jobs/{id}   │
    │                          ├──────────────────────▶│
    │                          │  Results + download   │
    │                          │◀──────────────────────┤
    │  Visualisation 3D        │                       │
    │◀─────────────────────────┤                       │
5.4 Gestion des Jobs
La gestion des jobs de simulation est un enjeu critique : un job FEM 3D peut durer de 30 secondes à plusieurs heures. Le système doit gérer la concurrence, la priorisation, la résilience et le nettoyage des ressources.
•	File d'attente prioritaire : RabbitMQ avec trois queues (high, normal, low). Les identifications 1D passent en high (retour rapide), les simulations 3D en normal, les batch overnight en low.
•	Pool de workers : autoscaling Kubernetes Horizontal Pod Autoscaler basé sur la longueur de queue et l'usage CPU. Limite maximale configurable pour maîtriser le coût cloud.
•	Retry & idempotence : chaque job a un UUID déterministe. En cas de crash worker, RabbitMQ redistribue le message ; le worker détecte via PostgreSQL si le job a déjà été (partiellement) traité, reprend à partir d'un checkpoint ou repart de zéro.
•	Observabilité : chaque étape du job écrit un log structuré (Loki), une métrique (Prometheus) et un span de trace (OpenTelemetry). Le dashboard Grafana permet de diagnostiquer un ralentissement en < 2 minutes.
5.5 Communication entre Services
Trois canaux de communication, choisis selon la nature de l'échange :
Canal	Usage	Avantages	Contraintes
REST / HTTP	Interactions synchrones frontend ↔ backend	Standard, outillage riche, debuggable	Latence, chaque appel = requête complète
gRPC	Inter-services backend haute fréquence (ex: API → Compute Engine pour fit rapide)	Binaire, streaming, contrats stricts (protobuf)	Moins debuggable, plus d'infrastructure
RabbitMQ (AMQP)	Asynchrone : jobs de simulation, notifications	Découplage, tolérance aux pannes, priorisation	Latence, complexité opérationnelle
WebSocket (STOMP)	Push temps réel frontend (progression, notifications)	Interactivité, faible latence	Gestion des reconnexions

📐 Principe architectural fondamental
Séparation stricte physique / numérique / infrastructure. Une loi matériau (ex: Prony) ne doit jamais dépendre du solveur qui l'utilise (FEM ou FVM), et aucun des deux ne doit dépendre de la base de données ou du framework HTTP. Cette discipline architecturale est la condition nécessaire pour que le projet puisse évoluer sur 5-10 ans sans réécriture majeure.
 
5.6 Décisions d'Architecture — Trade-offs Assumés
Toute architecture est un produit de compromis. Cette section documente les cinq décisions structurantes du projet, en présentant pour chacune les alternatives écartées, les compromis acceptés, et la justification finale. Ce format ADR (Architecture Decision Record) résumé permet de tracer la rationalité des choix et de les revisiter consciemment si le contexte évolue.
ADR-1 — C++ pour le Compute Engine (vs Python, Rust)
Décision : le compute engine est implémenté en C++20.
Alternatives considérées
Option	Forces	Pourquoi écartée
Python (numpy/scipy)	Vitesse de développement, écosystème scientifique mature, lisibilité	Performance insuffisante en hot loop FEM (facteur ×30 à ×100 vs C++), GIL, pas de zero-cost abstractions, risque de devoir tout réécrire en V3
Rust	Sécurité mémoire, performance équivalente à C++, ergonomie moderne	Écosystème scientifique immature (pas d'équivalent PETSc/Trilinos), marché du recrutement étroit, interop FFI moins fluide pour wrappers Python
Julia	Expressivité scientifique, performance JIT proche de C++	Maturité production limitée, taille de communauté insuffisante, coût de démarrage JVM-like, exotisme face aux DSI industrielles

Compromis acceptés : courbe d'apprentissage plus raide pour les nouveaux développeurs, gestion mémoire manuelle (mitigée par smart pointers et sanitizers en CI), temps de compilation plus long.
Justification : la performance brute est non-négociable pour la simulation 3D V2/V3, l'écosystème scientifique C++ (Eigen, PETSc, MFEM, OpenMP, MPI) est inégalé, et l'interop avec Python via pybind11 reste fluide pour les utilisateurs power-user. Décision robuste à long terme.
ADR-2 — RabbitMQ pour la Messagerie (vs Kafka, Redis Streams)
Décision : RabbitMQ 3.12 comme broker principal pour la file de jobs et les événements asynchrones.
Alternatives considérées
Option	Forces	Pourquoi écartée
Apache Kafka	Throughput massif (10M+ events/sec), streaming, replay event-sourcing	Sur-dimensionné pour notre profil (100-10 000 jobs/jour), pas de priorités natives, coût opérationnel lourd (Zookeeper / KRaft, partitioning, retention policies)
Redis Streams	Simplicité, latence sub-milliseconde, déjà présent comme cache	Pas de garanties de persistance équivalentes, retry / dead-letter moins riches, monitoring moins outillé
AWS SQS / Cloud Pub/Sub	Zéro ops, scalabilité automatique	Verrouillage cloud, pas portable on-prem (besoin entreprise), coût croissant linéaire avec le volume

Compromis acceptés : pas de capacités de streaming temps réel à très haut débit (non nécessaires ici), throughput plafonné autour de 50k msg/s par nœud (très au-dessus de nos besoins).
Justification : notre cas d'usage est centré sur des unités de travail discrètes (un job = une simulation), avec besoin de priorités (high/normal/low), retry contrôlé, dead-letter, et monitoring riche. RabbitMQ excelle exactement sur ce profil. Migration vers Kafka possible si le volume dépasse 1M jobs/jour — peu probable avant V4.
ADR-3 — FEM Prioritaire, FVM en Extension (vs FVM dès V1)
Décision : le moteur FEM est développé en priorité et constitue le solveur structural principal. La FVM est introduite en V2 pour la thermique et en V3 pour le couplage thermo-visco-élastique.
Alternatives considérées
•	FVM en parallèle dès V1 (parité dès le départ) : doublerait l'effort de développement sans bénéfice utilisateur immédiat — la mécanique des solides est largement dominée par FEM dans l'industrie.
•	FVM-only en s'inspirant d'OpenFOAM : risque scientifique élevé (FVM pour solides en grandes déformations est encore un sujet de recherche), perte de l'avantage écosystème FEM mature.
•	Wrapping d'un solveur tiers (Code_Aster, Calculix) : dépendance forte, moins de différenciation, complexité d'intégration importante.
Compromis acceptés : absence temporaire de capacités CFD ou couplages multiphysiques avancés en V1-V2.
Justification : le marché cible (visco-élasticité solide) attend FEM par défaut. Les benchmarks de référence (NAFEMS) sont formulés en FEM. Les exports Abaqus/ANSYS sont natifs en FEM. L'investissement FVM est justifié uniquement quand la couche thermique devient un point de douleur utilisateur — projeté en V2/V3.
ADR-4 — Monolithe Spring Boot en V1, Microservices en V2
Décision : la V1 est livrée comme un monolithe modulaire Spring Boot. La décomposition en 5 microservices (Project, Material, Data, Job, Report) intervient en V2 quand la pression de scalabilité et le découplage d'équipes la justifient.
Alternatives considérées
•	Microservices dès V1 : tentation classique d'« architecture parfaite dès le départ ». Coût caché énorme : infrastructure Kubernetes, observabilité distribuée, complexité de debugging, dette de coordination. Pour 3 utilisateurs pilotes, c'est du sur-engineering pur.
•	Monolithe permanent : interdirait la scalabilité indépendante du compute engine, du stockage objet et de l'API, posant un plafond technique en V3.
•	Architecture serverless (Lambda / Cloud Functions) : compute engine C++ avec runtime long mal adapté, démarrage à froid problématique, verrouillage cloud.
Compromis acceptés : nécessité d'un refactoring contrôlé entre V1 et V2 — accepté car les bounded contexts sont identifiés dès le design V1 (modules Maven séparés, pas de tables partagées entre contextes), ce qui rend la décomposition mécanique.
Justification : règle de Sam Newman : « ne décomposez en microservices que quand la douleur du monolithe devient supérieure à la complexité du distribué ». Pour 0-50 utilisateurs en V1, le monolithe est strictement supérieur. La transition V2 est planifiée et budgétée (~6 semaines d'effort).
ADR-5 — Angular + Spring Boot (vs React + Node, vs Vue + .NET)
Décision : Angular 17 (frontend) + Spring Boot 3 / Java 21 (backend).
Alternatives considérées
Stack	Forces	Pourquoi écartée
React + Node.js	Ecosystème colossal, flexibilité maximale, popularité	Moins opinionated → plus de décisions à prendre, écosystème JS fragmenté, Node moins adapté aux services lourds long-running, typage plus tardif
Vue.js + .NET / Python	Vue ergonomique, .NET mature, Python rapide à prototyper	Vue moins outillé pour applications enterprise complexes, .NET moins universel chez les clients européens, Python backend monolithique pose problème de scalabilité tardif
Svelte + Go	Performance frontend imbattable, Go simple et rapide	Écosystème Svelte encore jeune, Go peu présent dans les écosystèmes scientifiques (peu de bibliothèques rhéologie), recrutement plus difficile

Compromis acceptés : Angular est plus opinionated et impose plus de cérémonie qu'une stack React minimale ; Spring Boot a un footprint mémoire JVM plus élevé qu'un service Go ou Rust. Acceptés en échange de la maturité enterprise.
Justification : le couple Angular + Spring Boot est éprouvé sur des applications enterprise complexes, dispose d'une gouvernance long-terme (Google, Pivotal/VMware), excellent pour les domaines à forte logique métier (signals Angular, Spring Data JPA pour mapping objet-relationnel rhéologique). Java 21 avec virtual threads gomme l'écart de performance avec Node sur les workloads I/O-bound.

📐 Méthode ADR — bonne pratique à institutionnaliser
Chaque décision d'architecture significative doit être consignée comme un ADR (Architecture Decision Record) versionné dans le repo, au format Markdown, suivant un template uniforme : Contexte → Décision → Alternatives → Compromis → Conséquences.

Cette discipline a deux bénéfices : (1) onboarding accéléré des nouveaux développeurs (« pourquoi diable a-t-on choisi RabbitMQ ? »), (2) capacité à revisiter une décision si le contexte change (« en V4, le volume justifie peut-être Kafka »).
5.7 Diagrammes d'Architecture Complémentaires
Quatre diagrammes textuels précisent la vision déjà exposée en §5.1 et §5.3, en zoomant sur des aspects critiques pour l'implémentation.
Diagramme A — Architecture Microservices Détaillée (cible V2)
                         ┌─────────────────────────┐
                         │   Angular Frontend SPA  │
                         │   (PWA, VTK.js, NgRx)   │
                         └──────────┬──────────────┘
                                    │ HTTPS + WSS
                                    ▼
                         ┌─────────────────────────┐
                         │   API Gateway (Spring   │
                         │   Cloud Gateway)        │
                         │   • Rate limiting       │
                         │   • OpenAPI aggregation │
                         │   • OAuth2 enforcement  │
                         └──┬───┬───┬───┬───┬──────┘
                            │   │   │   │   │
         ┌──────────────────┘   │   │   │   └────────────────┐
         │                      │   │   │                    │
         ▼                      ▼   ▼   ▼                    ▼
  ┌────────────┐        ┌────────────┐ ┌────────────┐ ┌────────────┐
  │  Project   │◀──────▶│  Material  │ │    Job     │ │   Report   │
  │  Service   │  REST  │  Service   │ │  Service   │ │  Service   │
  │            │        │            │ │            │ │            │
  │ projects   │        │ materials  │ │ jobs       │ │ reports    │
  │ teams      │        │ models     │ │ runs       │ │ templates  │
  │ users      │        │ params     │ │ logs       │ │ exports    │
  └─────┬──────┘        └─────┬──────┘ └─────┬──────┘ └─────┬──────┘
        │                     │              │              │
        │                     ▼              │              │
        │              ┌────────────┐        │              │
        │              │    Data    │        │              │
        │              │  Service   │        │              │
        │              │ datasets   │        │              │
        │              │ experiments│        │              │
        │              └─────┬──────┘        │              │
        │                    │               │              │
        ▼                    ▼               ▼              ▼
   ┌───────────────────────────────────────────────────────────┐
   │   Infrastructure layer                                    │
   │  ┌─────────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐  │
   │  │ PostgreSQL  │ │  Redis   │ │ MinIO/S3 │ │ RabbitMQ │  │
   │  │+TimescaleDB │ │ (cache)  │ │ (objects)│ │ (jobs)   │  │
   │  └─────────────┘ └──────────┘ └──────────┘ └────┬─────┘  │
   └────────────────────────────────────────────────┬┘─────────┘
                                                    │
                                                    ▼
                                       ┌─────────────────────────┐
                                       │   Compute Engine Pool   │
                                       │   (C++20, gRPC server)  │
                                       │   N workers autoscaled  │
                                       └─────────────────────────┘

Diagramme B — Flux de Simulation End-to-End
USER          FRONTEND       GATEWAY    JOB-SVC    RABBITMQ   COMPUTE    MINIO    REPORT-SVC
│             │              │          │          │          │          │        │
├─Click Run──▶│              │          │          │          │          │        │
│             │─POST /jobs──▶│          │          │          │          │        │
│             │              │─/jobs───▶│          │          │          │        │
│             │              │          │─INSERT───┼──────────┼──────────┼───▶DB   │
│             │              │          │─publish─▶│          │          │        │
│             │              │◀─201 Created        │          │          │        │
│             │◀─202 Created │          │          │          │          │        │
│◀───toast───│              │          │          │          │          │        │
│             │                                    │          │          │        │
│             │                                    │─consume─▶│          │        │
│             │                                    │          │─fetch───▶│        │
│             │                                    │          │◀─mesh+case│        │
│             │                                    │          │          │        │
│             │                                    │          ├─[FEM loop]         │
│             │                                    │          ├─[checkpoints]      │
│             │                                    │          ├─[snapshots]        │
│             │                                    │          │          │        │
│             │                                    │          │─upload──▶│        │
│             │◀─WSS progress events from Job-Svc─┼──────────┼──────────┤        │
│◀──progress─│                                    │          │          │        │
│             │                                    │          │─done────▶│        │
│             │                                    │─UPDATE──┐│          │        │
│             │                                    │  job=OK ││          │        │
│             │◀─WSS notif: job done──────────────┘│          │          │        │
│◀──ready────│                                    │          │          │        │
│             │                                                                    │
├─Generate─▶─│─POST /reports────────────────────────────────────────────────────▶│
│  report    │                                                                    │
│             │                                                                    ├─render PDF
│             │                                                                    ├─pull artifacts from MinIO
│             │◀────────────────────────────────────────────────────PDF URL──────│
│◀──download─│                                                                    │

Diagramme C — Pipeline du Compute Engine (FEM)
  INPUT                          PROCESSING                          OUTPUT
  ─────                          ──────────                          ──────
                                                                     
  case.json ───┐                                                     
               │                                                     
               ▼                                                     
         ┌───────────┐    ┌────────────┐    ┌────────────────┐      
         │   PARSE   │───▶│  VALIDATE  │───▶│  LOAD MATERIAL │      
         │ JSON+Schema│    │  invariants│    │  (constitutive)│      
         └───────────┘    └────────────┘    └────────┬───────┘      
                                                     │              
  mesh.msh ───┐                                      │              
              │                                      │              
              ▼                                      ▼              
        ┌───────────┐     ┌────────────┐    ┌────────────────┐      
        │ READ MESH │────▶│ ASSEMBLE   │───▶│ APPLY BOUNDARY │      
        │  (Gmsh)   │     │   K, M, C  │    │   CONDITIONS   │      
        └───────────┘     └────────────┘    └────────┬───────┘      
                                                     │              
                                                     ▼              
                          ┌────────────────────────────────────┐    
                          │  TIME-STEPPING LOOP   t = t + Δt   │    
                          │  ┌──────────────────────────────┐  │    
                          │  │  Predict u_pred              │  │    
                          │  │  Newton-Raphson iteration    │  │    
                          │  │   ├─ Compute residual r      │  │    
                          │  │   ├─ Constitutive update     │  │    
                          │  │   │   per Gauss point        │  │    
                          │  │   ├─ Tangent operator        │  │    
                          │  │   ├─ Solve K·Δu = r          │  │    
                          │  │   ├─ Update u, q_i           │  │    
                          │  │   └─ Check convergence       │  │    
                          │  ├──────────────────────────────┤  │    
                          │  │  Checkpoint every N steps    │  │    
                          │  │  Write snapshot every M sec  │  │    
                          │  └──────────────────────────────┘  │    
                          └─────────────────┬──────────────────┘    
                                            │                       
                                            ▼                       
                                   ┌─────────────────┐    ───────▶ result.vtu
                                   │  POST-PROCESS   │    ───────▶ probes.csv
                                   │  • Probes       │    ───────▶ summary.json
                                   │  • Invariants   │    ───────▶ run.log
                                   │  • Energies     │              
                                   └─────────────────┘              

Diagramme D — Lifecycle d'un case.json
             ┌─────────────────────────────────────┐
             │        ÉTAT INITIAL : DRAFT         │
             │  case.json créé en mémoire frontend │
             │  pas encore validé, pas persisté    │
             └────────────────┬────────────────────┘
                              │  user clicks Save
                              ▼
             ┌─────────────────────────────────────┐
             │       ÉTAT : VALIDATED              │
             │  Schema JSON OK, persisté en DB     │
             │  case_id généré, checksum calculé   │
             └────────────────┬────────────────────┘
                              │  user clicks Run
                              ▼
             ┌─────────────────────────────────────┐
             │        ÉTAT : QUEUED                │
             │  Publié sur RabbitMQ, en attente    │
             │  d'un worker disponible             │
             └────────────────┬────────────────────┘
                              │  worker picks up
                              ▼
             ┌─────────────────────────────────────┐
             │        ÉTAT : RUNNING               │
             │  Compute engine en cours d'exécution│
             │  Logs streamés, progress publié WSS │
             └────────┬───────────────────┬────────┘
                      │                   │
      success ────────┘                   └──── failure / cancel
                      │                   │
                      ▼                   ▼
       ┌───────────────────────┐   ┌─────────────────────┐
       │  ÉTAT : COMPLETED     │   │  ÉTAT : FAILED      │
       │  Résultats dans MinIO │   │  Stack trace logged │
       │  Notification user    │   │  Retry possible 3x  │
       │  Disponible 90 jours  │   │  Diagnostic UI      │
       └──────────┬────────────┘   └─────────────────────┘
                  │  90 days TTL
                  ▼
       ┌───────────────────────┐
       │  ÉTAT : ARCHIVED      │
       │  Snapshots → Glacier  │
       │  case.json conservé   │
       │  indéfiniment (cheap) │
       │  Restore possible 24h │
       └───────────────────────┘

Garanties :
  • IMMUTABILITÉ : un case.json en état VALIDATED ne peut plus être modifié,
                   seulement cloné (création d'un nouveau case_id).
  • REPRODUCTIBILITÉ : rejouer un case.json en état COMPLETED produit un
                       résultat bit-exact (à epsilon documenté près).
  • TRAÇABILITÉ : chaque transition d'état est journalisée (audit trail).

🔐 Pourquoi ces 4 diagrammes ?
Le diagramme A clarifie la cible architecturale V2 et conditionne les recrutements (compétences microservices).
Le diagramme B sert de référence aux développeurs full-stack pour comprendre le couplage frontend/backend/compute.
Le diagramme C est le contrat entre l'équipe scientifique et l'équipe C++ : ce qui est dans la boucle, ce qui ne l'est pas.
Le diagramme D est la base juridique de la promesse de reproductibilité — sans cycle de vie strict, pas de bit-exactness.
PARTIE 6 — Architecture Scientifique
6.1 Modèles Visco-Élastiques
Le cœur scientifique de RheoSim Enterprise repose sur une hiérarchie de modèles constitutifs rigoureusement formulés. Chaque modèle est implémenté comme une classe concrète héritant d'une interface ConstitutiveLaw commune, garantissant l'interchangeabilité et la composabilité.
Modèle 1 — Maxwell (ressort + dashpot en série)
Le modèle de Maxwell combine un ressort linéaire et un amortisseur visqueux en série. Sous déformation imposée ε(t), la contrainte suit l'équation différentielle :
σ̇/E + σ/η = ε̇         (équation de Maxwell)

Réponse à ε₀ constante (relaxation) :
σ(t) = E · ε₀ · exp(-t/τ)    avec τ = η/E

Réponse à σ₀ constante (fluage) :
ε(t) = σ₀/E + (σ₀/η) · t    (fluage illimité — limitation du modèle)
Domaine de validité : excellent pour la relaxation de contrainte de fluides visco-élastiques (polymères fondus, gels). Limité pour les solides : prédit un fluage non borné, ce qui est physiquement faux pour la plupart des solides visco-élastiques.
Modèle 2 — Kelvin-Voigt (ressort + dashpot en parallèle)
Le modèle de Kelvin-Voigt combine le ressort et l'amortisseur en parallèle. Sous contrainte imposée σ(t) :
σ = E · ε + η · ε̇       (équation de Kelvin-Voigt)

Réponse à σ₀ constante (fluage) :
ε(t) = (σ₀/E) · [1 - exp(-t/τ)]    avec τ = η/E

Réponse à ε₀ constante (relaxation) :
σ(t) = E · ε₀       (réponse instantanée, puis constante — limitation)
Domaine de validité : excellent pour le fluage de solides visco-élastiques (caoutchoucs, élastomères réticulés). Limité pour la relaxation : ne décrit pas la décroissance de contrainte observée expérimentalement.
Modèle 3 — Série de Prony (Maxwell généralisé)
La série de Prony est le standard de facto dans l'industrie et la FEA. Elle combine N éléments Maxwell en parallèle avec un ressort d'équilibre :
Module de relaxation :
E(t) = E∞ + Σᵢ₌₁ᴺ Eᵢ · exp(-t/τᵢ)

Forme fréquentielle (DMA) :
E'(ω) = E∞ + Σᵢ Eᵢ · (ωτᵢ)² / (1 + (ωτᵢ)²)     [stockage]
E''(ω) = Σᵢ Eᵢ · (ωτᵢ) / (1 + (ωτᵢ)²)           [perte]
tan δ(ω) = E''(ω) / E'(ω)

Compliance de fluage (formulation duale) :
J(t) = 1/E∞ - Σⱼ Jⱼ · exp(-t/λⱼ)    (Prony pour le fluage)
Domaine de validité : universel. Avec N suffisant (typiquement 3 à 7 branches, décade par décade), Prony fitte fidèlement toute donnée visco-élastique linéaire, en relaxation, fluage, ou DMA. C'est le modèle prioritaire de RheoSim Enterprise.
Modèle 4 — Burgers (combinaison)
Modèle Maxwell + Kelvin-Voigt en série, utile pour matériaux bitumineux et composites à fluage primaire + secondaire. Implémenté en phase 2.
Modèle 5 — Fractionnaire Scott-Blair (phase 3)
Les modèles fractionnaires (dérivées d'ordre non-entier α ∈ ]0,1[) décrivent des comportements visco-élastiques auto-similaires difficiles à capturer avec un petit nombre d'éléments Prony. Plus exigeants numériquement (opérateurs de mémoire, convolution avec noyau de Mittag-Leffler). Implémentation différée — cible utilisateurs recherche avancée.
6.2 Types d'Expériences Supportées
Chaque expérience est un protocole précisément défini, exécutable aussi bien comme simulation (avec un modèle) que comme identification (avec des données réelles).
Expérience	Variable imposée	Variable mesurée	Phase cible	Modèles adaptés
Fluage (creep)	σ = σ₀ (échelon)	ε(t)	MVP	Kelvin-Voigt, Prony (fluage), Burgers
Relaxation	ε = ε₀ (échelon)	σ(t)	MVP	Maxwell, Prony (relaxation)
Cyclique	ε(t) triangulaire ou sinus	σ(t)	V1	Tous (pour hystérésis)
DMA	ε(t) = ε₀ sin(ωt), balayage ω	σ(t) → E'(ω), E''(ω), tan δ	V1	Prony (calibrage de référence)
TTSP	DMA multi-température	Master curve + shift factors aT(T)	V2	Prony + WLF / Arrhenius
Traction quasi-statique	ε̇ constant (lent)	σ(ε)	MVP	Tous (module de référence)
Compression / cisaillement	idem adapté	idem	V1	Tous

6.3 Principe FEM vs FVM
Méthode des Éléments Finis (FEM) — moteur prioritaire
La FEM repose sur la formulation faible du problème d'équilibre mécanique. Le domaine est discrétisé en éléments (tétraèdres, hexaèdres), le champ de déplacement est interpolé par des fonctions de forme polynomiales N_i, et l'équilibre est imposé au sens des résidus pondérés (Galerkin). Cela conduit à un système algébrique K(u)·u = f, résolu par Newton-Raphson quand le matériau est non-linéaire.
Pour un matériau visco-élastique, la difficulté réside dans l'intégration temporelle du modèle constitutif à chaque point de Gauss. À chaque pas de temps Δt, on dispose de l'état précédent (contrainte, déformation, variables internes q_i). On calcule l'incrément de déformation, on met à jour les variables internes via un schéma implicite (recurrence exponentielle pour Prony, très efficace), on obtient la nouvelle contrainte et — crucial pour la convergence de Newton — l'opérateur tangent constitutif ∂σ/∂ε.
Méthode des Volumes Finis (FVM) — extension phase 2-3
La FVM discrétise le domaine en volumes de contrôle et impose les bilans de flux sur les faces. Elle est dominante en CFD et en thermique. Pour la mécanique des solides, la FVM existe (travaux de Jasak, Demirdžić) mais reste minoritaire. Dans RheoSim, la FVM est proposée comme extension pour :
•	La thermique (calcul de la distribution de température dans une pièce, couplée à la visco-élasticité via la méthode TTSP locale).
•	Les couplages multiphysiques (thermo-visco-élasticité, structure-fluide via FSI).
•	L'interopérabilité OpenFOAM (écosystème FVM mature).
Position technique claire
FEM reste le moteur principal pour la mécanique visco-élastique des solides. La FVM, techniquement plus complexe pour ce domaine, est introduite d'abord sur la thermique, puis en couplage. Nous n'essaierons pas de faire de la FVM structurelle pure — ce serait un surengineering coûteux pour un bénéfice marginal.
6.4 Gestion des Variables Internes
Les modèles visco-élastiques à mémoire (Prony en particulier) nécessitent de stocker un état interne qui évolue dans le temps. Pour une série de Prony à N branches, on stocke pour chaque point de Gauss N tenseurs internes q_i (contraintes partielles sur chaque branche Maxwell).
Mise à jour incrémentale (schéma exponentiel, inconditionnellement stable) :

  q_i(n+1) = exp(-Δt/τ_i) · q_i(n)
          + E_i · [1 - exp(-Δt/τ_i)] · Δε

  σ(n+1) = E∞ · ε(n+1) + Σᵢ q_i(n+1)

Avantage : pas de sous-itération, pas de limite CFL, ordre 2 en temps.
Coût mémoire : 6·N floats par point de Gauss (tenseur symétrique 3D × N branches).

Pour un maillage 100k éléments × 8 Gauss × Prony-5 :
  100000 × 8 × 6 × 5 × 8 octets = 192 Mo d'état interne
  → gérable en RAM, mais doit être persisté pour reprise sur checkpoint.
Cette discipline de « état local au point de Gauss » est ce qui rend le compute engine agnostique au solveur (FEM ou FVM) : peu importe comment on calcule Δε, la mise à jour constitutive est locale et identique.
6.5 Pipeline de Simulation
Le pipeline canonique d'une simulation 3D visco-élastique se décompose en neuf étapes, chacune associée à un module dédié dans le compute engine :
8.	Parsing du case.json — validation stricte via JSON Schema, chargement des paramètres.
9.	Chargement du maillage — depuis MinIO, formats acceptés : .msh (Gmsh), .vtu (VTK), .inp (Abaqus).
10.	Construction des matrices globales — assemblage K (rigidité), M (masse), C (amortissement si dynamique).
11.	Initialisation du temps — t=0, état interne q_i=0, déplacement u=0.
12.	Boucle temporelle — pour chaque Δt : prédiction, correction Newton-Raphson si non-linéaire, mise à jour des variables internes.
13.	Convergence — critère combiné résidu force + incrément déplacement.
14.	Écriture des résultats — snapshot VTU à intervalles configurés, état interne persisté pour reprise.
15.	Post-traitement — extraction de sondes, invariants, énergies.
16.	Publication — upload des artefacts vers MinIO, notification RabbitMQ, mise à jour du statut en base.
Chaque étape est instrumentée : métriques Prometheus (temps, mémoire, itérations), logs structurés, et span OpenTelemetry. Cela permet un diagnostic précis en production.
6.6 Stratégie de Validation Scientifique
Un simulateur scientifique n'a de valeur que s'il est validé. Trois niveaux de validation, gradués :
Niveau 1 — Tests unitaires (solutions analytiques)
Chaque modèle constitutif est vérifié contre sa solution analytique : fluage Kelvin-Voigt 1D, relaxation Maxwell 1D, réponse DMA Prony-1. Ces tests sont exécutés à chaque commit (CI). Tolérance : erreur relative < 10⁻⁶.
Niveau 2 — Tests de validation croisée
Cas tests standards issus de la littérature et de NAFEMS : cylindre creux sous pression interne visco-élastique (solution semi-analytique), éprouvette en traction relaxation multi-axiale. Comparaison RheoSim vs Abaqus. Tolérance : < 2% d'écart sur grandeurs intégrales.
Niveau 3 — Benchmarks expérimentaux
Campagnes expérimentales réalisées avec un laboratoire partenaire (à sécuriser en phase 2) : fluage 10⁵ s sur éprouvettes PA6 et EPDM, DMA multi-température sur PC. Publication peer-reviewed de ces benchmarks comme référence communautaire.
 
PARTIE 7 — Roadmap
7.1 Principes de la Roadmap
La roadmap s'articule en trois versions majeures, correspondant à trois niveaux de maturité produit. Le découpage respecte deux règles strictes : (1) chaque version est vendable / utilisable en l'état, (2) chaque version ferme un scope avant d'ouvrir le suivant. Cette discipline évite le syndrome classique du projet scientifique ambitieux qui ne sort jamais.
Règle d'or
V1 doit être en production chez trois utilisateurs externes AVANT que V2 ne soit planifiée en détail. Le feedback terrain réel invalidera au moins 20 % des hypothèses produit initiales.
7.2 V1 — MVP Réaliste (0 → 6 mois)
Objectif V1
Délivrer un outil 1D utilisable en production, qui couvre le workflow « import CSV → identification paramétrique Maxwell/Kelvin-Voigt/Prony → comparaison → export ». Pas de 3D, pas d'IA avancée, pas de multi-utilisateur. Objectif : prouver que le noyau fonctionne et gagner les premiers utilisateurs pilotes.
Périmètre fonctionnel V1
•	Modèles : Maxwell, Kelvin-Voigt, Prony-N (N=1 à 10).
•	Expériences : fluage, relaxation, traction quasi-statique.
•	Identification : L-BFGS-B avec contraintes (scipy / NLopt), pas de ML encore.
•	Import : CSV, Excel basique.
•	Export : CSV, JSON, PNG graphiques, rapport PDF simple.
•	UI : Angular monolithique, pas de collaboration, authentification simple (email + mot de passe).
•	Backend : Spring Boot monolithique (pas encore découpé en microservices), PostgreSQL unique.
•	Infrastructure : docker-compose local, Heroku ou Scaleway pour démonstrations.
Ce qui n'est PAS dans V1
•	Pas de 3D FEM.
•	Pas de DMA ni TTSP (évaluer selon feedback — possible en V1.5).
•	Pas d'active learning ni de model recommender.
•	Pas de bibliothèque de matériaux collaborative.
•	Pas de Kubernetes ni de haute disponibilité.
Livrables V1
Livrable	Critère d'acceptation
Version v0.1.0 déployée	Accessible en ligne, authentification fonctionnelle, 0 bug bloquant
3 utilisateurs pilotes	Ayant réalisé au moins une identification complète sur leurs données
Documentation utilisateur	Guide d'utilisation 30 pages + 3 tutoriels vidéo
Tests unitaires	Couverture > 70% sur le core physique, > 50% sur l'API
Benchmarks analytiques	10 cas tests passés avec tolérance < 10⁻⁵

7.3 V2 — Version Avancée (6 → 18 mois)
Objectif V2
Transformer l'outil 1D en plateforme scientifique complète, introduire la 3D FEM, les fonctionnalités DMA/TTSP, les premières briques d'IA (Auto-Fit, Model Recommender), et passer à une architecture microservices scalable. Objectif commercial : passer de 3 utilisateurs pilotes à 50 utilisateurs payants.
Périmètre fonctionnel V2
•	Nouveaux modèles : Burgers, extension au cisaillement (G(t), tan δ), formulation isotrope 3D.
•	Nouvelles expériences : cyclique, DMA complet, TTSP avec shift WLF/Arrhenius.
•	Compute Engine 3D FEM : C++20 avec Eigen + CG/GMRES, maillage Gmsh .msh, champs σ/ε visualisables en VTK.
•	Auto-Fit IA v1 : initialisation ML + régularisation adaptative, gain ×3 à ×5 en vitesse de convergence.
•	Model Recommender v1 : classifieur Gradient Boosting, 3 à 5 recommandations avec probabilités.
•	Bibliothèque de matériaux : 50 matériaux pré-peuplés, versionning, recherche.
•	Architecture : découpage microservices (5 services), Kubernetes sur cluster dédié, observabilité Prometheus/Grafana.
•	Collaboration : équipes, permissions, partage de projets, commentaires sur graphiques.
•	Exports avancés : LaTeX snippets, Abaqus .inp, ANSYS .cdb, OpenFOAM dictionnaire.
Livrables V2
Livrable	Critère d'acceptation
Version v1.0.0 GA	Déployée en production sur cluster Kubernetes, SLA 99.5%
Compute Engine 3D	Benchmark NAFEMS validé à < 2% d'écart vs Abaqus
50 utilisateurs payants	Mixte recherche + industrie, 3 logos de clients industriels
Publication scientifique	1 article soumis dans Journal of Rheology ou équivalent
Partenariat laboratoire	Convention signée pour benchmarks expérimentaux

7.4 V3 — Vision Long Terme (18 → 36 mois)
Objectif V3
Positionner RheoSim Enterprise comme plateforme de référence en Europe sur la simulation visco-élastique. Ouverture multiphysique (couplage thermique prioritaire), exécution HPC pour gros modèles, mode SaaS multi-tenant, et écosystème de plugins communautaire. Objectif : 500 utilisateurs actifs, 15 clients entreprise, break-even financier.
Périmètre fonctionnel V3
•	Multiphysique : couplage thermo-visco-élastique complet, FVM thermique en C++, interpolation champ T sur maillage solide.
•	IA avancée : Active Learning pour planification expérimentale, Digital Twin matériau (agrégation de campagnes), TTSP neural pour raffinement shift factors, assistant d'analyse LLM local.
•	HPC : parallélisation OpenMP puis MPI, branchement PETSc, support maillages > 10⁶ DOFs, run distribué sur cluster HPC.
•	SaaS multi-tenant : isolation stricte par tenant, billing usage-based, SSO SAML pour grands comptes.
•	Écosystème plugins : SDK Python pour modèles personnalisés, marketplace, revenus partagés avec contributeurs.
•	Intégrations CAO : plugins Abaqus (pré-processeur), connecteur Salome, API pour intégration CATIA / NX.
•	Mode pédagogique complet : 30 scénarios guidés, partenariats universitaires, licences campus.
•	Mobile : app iOS/Android pour consultation des résultats, notifications, approbations workflow.
Livrables V3
Livrable	Critère d'acceptation
Version v2.0.0	Multi-tenant SaaS, 15 clients entreprise payants
Marketplace plugins	10 plugins tiers disponibles, 500 téléchargements/mois
HPC production	1 client exécutant sur cluster HPC externe (Jean Zay, GENCI, ou équivalent industriel)
Publications	3 articles peer-reviewed, présence ESR conference
Break-even	ARR > 1M€, coût d'acquisition clients < LTV / 3

7.5 Vue d'Ensemble et Jalons
Synthèse graphique des trois versions, jalons et indicateurs clés :
  Mois 0      3      6      9     12     15     18     24     30     36
  │          │      │      │     │      │      │      │      │      │
  ▼──────────▼      ▼      ▼     ▼      ▼──────▼      ▼      ▼      ▼
  ◆ V1 MVP ───────── ◆      │     │      │      │      │      │      │
  │  • Core 1D              │     │      │      │      │      │      │
  │  • 3 pilotes            │     │      │      │      │      │      │
  │                         │     │      │      │      │      │      │
  │          ◆ V2 Avancée ──┴─────┴──────◆      │      │      │      │
  │             • 3D FEM                        │      │      │      │
  │             • IA v1                         │      │      │      │
  │             • 50 users                      │      │      │      │
  │                                             │      │      │      │
  │                         ◆ V3 Vision Long ───┴──────┴──────┴──────◆
  │                            • Multiphysique                       │
  │                            • HPC + SaaS                          │
  │                            • 500 users, 15 entreprises           │

  Jalons de décision (go / no-go) :
   M6  → V1 GA • décider V2 scope selon feedback pilotes
   M18 → V2 GA • décider V3 investissement selon ARR atteint
   M24 → Break-even annuel visé, décision IPO/acquisition ou croissance organique
 
7.6 Scope Technique du Moteur de Calcul V1
La roadmap V1 a déjà décrit le périmètre fonctionnel global du MVP. Cette section zoome spécifiquement sur le compute engine — la partie scientifique critique — pour expliciter ce qui en fait partie et, surtout, ce qui en est volontairement exclu. La discipline de l'exclusion est ici plus importante que celle de l'inclusion : c'est elle qui protège le projet du sur-engineering.
Ce qui est INCLUS dans le compute engine V1
Modèles constitutifs
•	Maxwell simple (1 branche).
•	Kelvin-Voigt simple (1 branche).
•	Maxwell généralisé (Prony) jusqu'à N=10 branches.
•	Formulation isotrope linéaire uniquement (pas d'anisotropie, pas de grandes déformations).
•	Hypothèse petites déformations (formulation linéarisée HPP).
Discrétisation spatiale
•	1D pur : poutre / barreau homogène, pour relaxation, fluage, traction quasi-statique.
•	2D simple en quasi-statique : éprouvettes idéalisées (carré, rectangle), maillages triangulaires/quadrilatéraux générés en interne ou importés Gmsh.
•	Éléments de premier ordre uniquement (T3, Q4).
Discrétisation temporelle
•	Schéma exponentiel pour les variables internes Prony (recurrence stable inconditionnellement).
•	Pas de temps fixe ou adaptatif basique (heuristique simple).
Solveur linéaire
•	Direct Eigen SimplicialLDLT pour problèmes < 50k DOFs (largement suffisant pour 1D/2D simples).
•	CG basique en fallback pour les cas légèrement plus gros.
Identification paramétrique
•	L-BFGS-B via NLopt avec contraintes de positivité.
•	Levenberg-Marquardt en alternative pour les utilisateurs power.
•	Pas d'IA encore — initialisation par heuristique simple (uniformément distribué en log τ).
Entrées / sorties
•	case.json en lecture (schéma 1.0).
•	Mesh en .msh Gmsh basique.
•	Sortie : CSV séries temporelles + JSON résumé + log.

Ce qui est EXPLICITEMENT EXCLU du compute engine V1
Liste exhaustive des fonctionnalités techniquement séduisantes mais volontairement reportées. Si un membre de l'équipe propose d'ajouter l'une de ces fonctionnalités en V1, c'est un signal d'alarme.
Exclusion	Pourquoi tentant	Pourquoi reporté
3D FEM complet (T4, H8, H20)	Effet démonstration fort, demande utilisateur affichée	Coût d'implémentation 4-6 mois, validation NAFEMS lourde, le marché V1 (3 pilotes) accepte largement le 1D/2D
Grandes déformations (Lagrangien total)	Cas industriels élastomères réels	Complexité formulation × 5, débordement de scope, V2 minimum
Plasticité couplée à la visco-élasticité	Modèles plus réalistes	Hors thèse du projet (visco-élasticité linéaire/quasi-linéaire), reporté en V3+
Contact mécanique	Indispensable pour pièces assemblées	Discipline à part entière, nécessite équipe dédiée, V3
Rupture, endommagement, fatigue	Demandes industrielles fréquentes	Hors scope visco-élasticité pure, reporté en V3+ ou jamais
MPI / parallélisation distribuée	Performance HPC	Inutile sous 100k DOFs, complexifie le déploiement, V3
GPU (CUDA / HIP)	Performance impressionnante	Maturité écosystème scientifique GPU encore inégale, ROI faible avant gros maillages, V3
Multiphysique (thermo-mécanique)	Couplages réels matériaux polymères	Demande FVM mature, V2-V3
Préconditionneurs AMG (BoomerAMG, etc.)	Performance solveurs gros systèmes	Inutile sous 50k DOFs, intégration PETSc lourde, V3
Maillages adaptatifs (h-refinement)	Précision automatique	Complexité algorithmique majeure, V3 si demande forte
IA dans la boucle (Auto-Fit ML)	Différenciation marketing forte	Données d'entraînement à constituer, V2 obligatoire
Modèles fractionnaires (Scott-Blair)	Innovation scientifique	Cible utilisateur recherche niche, V3

Justification de cette discipline d'exclusion
Cette restriction radicale du scope V1 répond à trois objectifs complémentaires :
17.	Time-to-market réaliste — un compute engine V1 minimaliste mais robuste se livre en 4 mois avec 1 ingénieur senior C++. Le même engine avec 3D + plasticité + multiphysique demande 18 mois et 3 ingénieurs.
18.	Validation scientifique exhaustive — chaque ligne de code de V1 doit passer un benchmark analytique. Avec un scope réduit, l'équipe V1 a le temps de valider à fond. Avec un scope démesuré, on accumule de la dette scientifique invisible mais dévastatrice à terme.
19.	Apprentissage du vrai besoin utilisateur — la moitié des fonctionnalités exclues ne sera jamais demandée par les pilotes réels. Le coût de les avoir codées « au cas où » est colossal. Coder à la demande explicite est toujours moins cher que coder par anticipation.

⚠️ Discipline du NON
La règle d'or du chef de projet V1 : « Cette fonctionnalité est-elle indispensable pour les 3 utilisateurs pilotes du mois prochain ? » Si la réponse n'est pas un OUI évident et défendable, la fonctionnalité est exclue.

Cette discipline est inconfortable. Elle frustre les ingénieurs ambitieux. Elle peut donner l'impression d'un produit moins « impressionnant ». Mais elle est l'unique différence entre un projet qui sort en V1 et un projet qui meurt en intégration permanente.
PARTIE 8 — Document Technique (Complet)
Cette partie s'adresse aux développeurs, aux ingénieurs simulation et aux physiciens qui implémenteront, maintiendront ou étendront RheoSim Enterprise. Elle détaille les décisions techniques, les interfaces, les formats de données et les pièges à éviter.
8.1 Architecture Technique Détaillée
Stack technologique par couche
Couche	Stack	Justification technique
Frontend	Angular 17 (standalone, signals), TypeScript 5, VTK.js, Chart.js, NgRx	Angular pour maturité enterprise, VTK.js seul toolkit 3D scientifique web, signals pour granularité réactivité
API Gateway	Spring Cloud Gateway	Ingress unique, rate limiting, aggregation OpenAPI
Services API	Spring Boot 3, Java 21 (virtual threads), Spring Security, Spring Data JPA	JVM stabilité production, virtual threads pour I/O-bound, écosystème mature
Compute Engine	C++20, Eigen 3.4, NLopt, gRPC, CMake + Conan	Performance brute, zéro GC en hot loop, interop ecosysteme scientifique
Base de données	PostgreSQL 15 + TimescaleDB extension	ACID rigoureux, TimescaleDB pour séries temporelles (buckets, compression)
Cache	Redis 7	Session, résultats intermédiaires, pub/sub léger
Object storage	MinIO (on-prem) ou AWS S3 (SaaS)	Stockage scalable, versioning natif, compatible S3 API
Message broker	RabbitMQ 3.12	AMQP mature, priorités natives, monitoring riche
Identity	Keycloak 23	OIDC / SAML, SSO, MFA, self-hosted possible
Observability	Prometheus + Grafana + Loki + OpenTelemetry	Trio logs/metrics/traces standard CNCF
CI/CD	GitLab CI + ArgoCD	Pipeline complet, GitOps pour déploiements
Orchestration	Kubernetes 1.28+, Helm charts	Standard de facto, portabilité cloud / on-prem

8.2 Modules Techniques
Module Physics Core (C++)
Le Physics Core expose une interface abstraite commune aux deux moteurs de discrétisation. Principe : toute loi constitutive est locale au point de Gauss (ou à la cellule de contrôle), sans dépendance à la géométrie globale.
// Interface conceptuelle (simplifiée)
class IConstitutiveLaw {
public:
  virtual ConstitutiveState initialize() const = 0;

  // update: entrée = déformation totale + état(n) + dt
  //         sortie = contrainte(n+1) + état(n+1) + tangente
  virtual UpdateResult update(
    const StrainTensor& strain,
    const ConstitutiveState& state_n,
    double dt
  ) const = 0;

  virtual std::string modelId() const = 0;
  virtual ParameterSet parameters() const = 0;
};

// Implémentations : Maxwell, KelvinVoigt, Prony, Burgers, Fractional
// Chaque implémentation est unit-testée contre sa solution analytique.
Module Discretization Engines
Deux moteurs frères héritant d'une interface IDiscretizationEngine :
•	FemEngine : maillage éléments (T3, T4, T10, H8, H20), intégration Gauss 2×2×2 par défaut, assemblage K/M/C, Newton-Raphson.
•	FvmEngine : maillage polyédrique, flux sur faces, schémas centré ou upwind, en phase 2 thermique puis couplé.
Module Time Integrator
Schémas d'intégration temporelle supportés :
•	Euler implicite (robuste, ordre 1, pour quasi-statique).
•	Newmark (ordre 2, pour dynamique).
•	Generalized-α (amortissement numérique contrôlé, haute précision).
•	Schéma exponentiel interne pour les variables internes Prony (inconditionnellement stable).
Module Solver Linéaire
Pour le système linéarisé K·Δu = r à chaque itération Newton :
•	MVP : Eigen SimplicialLDLT (direct) jusqu'à 50k DOFs, ConjugateGradient (iteratif) au-delà.
•	V2+ : préconditionneurs diagonal / incomplete Cholesky, GMRES pour matrices non-symétriques.
•	V3 : branchement PETSc, préconditionneurs AMG (multigrille algébrique), support MPI distribué.
8.3 Formats de Données
Format case.json (format canonique RheoSim)
Le case.json est le document central : il contient tout ce qui est nécessaire pour reproduire une simulation. Validé par un JSON Schema strict (draft 2020-12). Exemple de structure :
{
  "schema_version": "1.0",
  "case_id": "uuid-...",
  "created_at": "2026-01-15T10:30:00Z",
  "created_by": "elise@acme.com",
  "checksum": "sha256:...",

  "material": {
    "id": "pa6-grade-A",
    "family": "polymer.thermoplastic",
    "model": {
      "type": "prony",
      "n_branches": 5,
      "E_inf": 2.1e9,
      "branches": [
        {"E": 1.3e9, "tau": 1.0},
        {"E": 0.8e9, "tau": 10.0},
        {"E": 0.5e9, "tau": 100.0}
      ],
      "temperature_ref": 298.15
    }
  },

  "experiment": {
    "type": "relaxation",
    "strain_amplitude": 0.01,
    "duration_s": 3600,
    "temperature_K": 298.15
  },

  "mesh": {
    "uri": "s3://bucket/meshes/specimen.msh",
    "checksum": "sha256:..."
  },

  "solver": {
    "engine": "fem",
    "time_integrator": "generalized-alpha",
    "dt": 0.1,
    "linear_solver": "cg",
    "newton_tol": 1e-6
  },

  "outputs": {
    "vtk_snapshots_hz": 1.0,
    "probes": ["node_top", "node_center"]
  }
}
Formats d'import
•	CSV : auto-détection séparateur (, ; \t), première ligne headers, unités inférées ou spécifiées (kPa, MPa, s, Hz).
•	Excel : prend la première feuille par défaut, mapping colonnes interactif si ambigu.
•	Formats DMA natifs : Anton Paar (.rpf), TA Instruments (.tri), Malvern (.msn). Parsers dédiés avec tests sur échantillons réels.
Formats d'export
•	CSV/JSON : séries temporelles + métadonnées.
•	VTK/VTU : champs 3D pour ParaView.
•	PDF : rapport Dublin Core, template LaTeX.
•	Abaqus .inp : bloc *VISCOELASTIC avec paramètres Prony.
•	ANSYS .cdb : fichier commande avec TB,PRONY.
•	OpenFOAM dictionary : dict pour rheologyProperties.
8.4 Pipeline de Calcul (Vue Développeur)
Job Service                   Compute Worker               MinIO          PostgreSQL
    │                               │                         │                │
    │ publish(job_id)               │                         │                │
    ├──────────────[RabbitMQ]──────▶│                         │                │
    │                               │ fetch case.json + mesh  │                │
    │                               ├────────────────────────▶│                │
    │                               │◀────────────────────────┤                │
    │                               │                         │                │
    │                               │ UPDATE jobs status=RUN  │                │
    │                               ├─────────────────────────┴───────────────▶│
    │                               │                                          │
    │                               │ [core loop]                              │
    │                               │   for t in 0..T:                         │
    │                               │     newton iterations                    │
    │                               │     update internal vars                 │
    │                               │     checkpoint every N steps             │
    │                               │                                          │
    │                               │ write vtk snapshots     │                │
    │                               ├────────────────────────▶│                │
    │                               │                         │                │
    │                               │ UPDATE jobs status=OK   │                │
    │                               ├─────────────────────────────────────────▶│
    │                               │                                          │
    │ NOTIFY (WebSocket)            │                                          │
    │◀──────────────────────────────┤                                          │
8.5 Gestion des Résultats
Les résultats d'une simulation sont structurés en trois niveaux, correspondant à trois besoins utilisateur :
•	Scalaires & sondes : évolution temporelle sur N points prédéfinis (typique < 100 MB, stocké en TimescaleDB pour interrogation rapide).
•	Champs 3D snapshots : fichiers VTU à N instants, stockés dans MinIO (typique 10-500 MB par snapshot, 5-50 snapshots par run).
•	État interne & checkpoints : pour reprise en cas de crash, ou analyse post-mortem, typique 100 MB - 10 GB.
Cycle de vie : les snapshots VTU sont conservés 90 jours par défaut, puis archivés en Glacier (S3 IA) ; les scalaires/sondes sont conservés indéfiniment. Configurable par projet en entreprise.
8.6 Risques Techniques
Risque	Description	Mitigation	Criticité
Convergence Newton	Le solveur FEM diverge sur des cas mal conditionnés	Line search, step halving, préconditionneurs adaptatifs, recommandation utilisateur	Haute
Identification non-unique	Plusieurs jeux de paramètres Prony minimisent le résidu	Régularisation Tikhonov, contraintes physiques, bornes littérature	Haute
Performance compute	Simulations 3D plus lentes qu'Abaqus	Profiling, vectorisation AVX, pré-assemblage, phase V3 PETSc/MPI	Moyenne
Dette technique rapide	Pression MVP → code rushé	Code reviews obligatoires, tests > 70%, refactor sprints	Moyenne
Dépendances externes	Keycloak, Eigen, VTK.js versions bloquantes	Versions épinglées, tests d'intégration, veille sécurité	Faible
Fuites mémoire C++	Simulations longues → crash worker	Smart pointers obligatoires, sanitizers en CI (ASan, UBSan)	Moyenne
Scalabilité DB	TimescaleDB saturée sur > 10⁹ points	Politique de rétention, archivage, partitionnement	Faible (tardif)

8.7 Recommandations d'Implémentation
20.	Commencer par le Physics Core en 1D pur, avant tout frontend. Validation analytique complète avant toute intégration.
21.	Écrire les tests d'intégration du pipeline complet (case.json → résultat) avant de développer la UI.
22.	Mettre en place la CI dès le jour 1 : lint, tests, coverage, sanitizers, validation JSON schema.
23.	Documenter les décisions architecturales dans des ADR (Architecture Decision Records) Markdown versionnés.
24.	Éviter la tentation de l'abstraction prématurée : coder le cas simple, refactorer quand le 3e cas apparaît.
25.	Monitorer dès le début les métriques produit (temps de fit, taux de convergence, taille de runs) — ce qui n'est pas mesuré ne peut pas être optimisé.
26.	Isoler le C++ dans son propre repo, avec son propre cycle de release. Contrat gRPC stable versionné.
27.	Ne pas sous-estimer le temps d'intégration : typiquement 40% du temps projet va dans les interfaces, pas dans les algorithmes.
 
8.8 Stratégie de Données (Data Strategy)
Les capacités d'IA évoquées dans la Partie 4 (Auto-Fit, Model Recommender, Active Learning, TTSP Neural) ne valent rien sans une stratégie de données rigoureuse. Cette section détaille les sources, les formats, le versionning, le pipeline de qualité et le stockage — éléments indispensables pour rendre la composante IA crédible et maintenable.
8.8.1 Sources de Données
Cinq sources alimentent l'écosystème de données RheoSim, chacune avec ses propres règles d'acquisition, de licence et de qualité.
Source	Nature	Licence type	Usage principal
NIST databases (PoLyInfo, MatWeb, NIST SRD)	Données publiques de référence, polymères industriels standards	Domaine public ou usage scientifique libre	Bibliothèque matériaux, jeu d'entraînement IA
Publications académiques (open access)	Datasets supplémentaires extraits de papers Elsevier, Wiley, ACS	CC-BY pour open access	Validation, jeux de test variés
Laboratoires partenaires	Campagnes expérimentales contractualisées (PA6, EPDM, PEEK, composites)	Accord bilatéral, co-publication	Benchmarks haute qualité, papers de référence
Clients industriels	Données privées propriétaires uploadées dans leur tenant	Confidentielle stricte (NDA), ne jamais sortir du tenant	Personnalisation par tenant, pas d'utilisation cross-tenant
Synthétique (simulation)	Datasets générés par RheoSim lui-même pour augmentation IA	Interne	Augmentation jeu d'entraînement, tests de robustesse

🛡️ Frontière éthique critique
Les données client (source 4) NE PEUVENT JAMAIS sortir du tenant pour entraîner un modèle global, même anonymisées. Cette règle est non-négociable, elle conditionne la confiance industrielle. Les modèles IA globaux (Auto-Fit, Recommender) s'entraînent uniquement sur les sources 1, 2, 3 et 5.
8.8.2 Format Interne Recommandé
Format binaire columnaire pour la performance et la portabilité, avec métadonnées riches en sidecar JSON :
DATASET = un répertoire structuré :

  pa6_grade_a_DMA_25C_2024-03-15/
    ├── data.parquet         # données numériques colonne-orientée
    │     columns: time_s, freq_hz, T_K, strain_%, stress_MPa,
    │              storage_modulus_MPa, loss_modulus_MPa, tan_delta
    ├── metadata.json        # métadonnées Dublin Core + RheoSim
    │     {
    │       "dc:title": "DMA sweep PA6 GradeA at 25°C",
    │       "dc:creator": "...",
    │       "dc:date": "2024-03-15",
    │       "dc:rights": "CC-BY 4.0",
    │       "rheo:material_family": "polymer.thermoplastic",
    │       "rheo:experiment_type": "DMA",
    │       "rheo:instrument": "Anton Paar MCR 702",
    │       "rheo:operator": "...",
    │       "rheo:protocol": "ISO 6721-4",
    │       "rheo:checksum_sha256": "...",
    │       "rheo:quality_score": 0.94
    │     }
    └── raw/                 # fichiers bruts machine, conservés tels quels
          └── original.rpf

POURQUOI PARQUET :
  • Compression automatique (snappy / zstd) → divise la taille par 5 à 10
  • Lecture colonne-par-colonne ultra-rapide pour pandas / polars / Arrow
  • Schéma typé (vs CSV no-schema)
  • Compatible écosystème data science (sklearn, pytorch via dataloader)
  • Format ouvert standardisé Apache, pérennité long terme
8.8.3 Versionning des Datasets
Les datasets évoluent : nouvelles campagnes, corrections d'erreurs, ajout de métadonnées. Sans versionning rigoureux, les modèles IA deviennent ingérables (« sur quel dataset le modèle v3 a-t-il été entraîné ? »). Trois choix sont compatibles avec notre stack :
•	DVC (Data Version Control) : intégration native Git, hash de contenu, remote S3 supporté. Excellent pour datasets jusqu'à ~100 GB. Recommandé V1-V2.
•	LakeFS : git-like sur object storage S3/MinIO, branches, merges, atomic commits. Plus complexe mais scalable au pétaoctet. Cible V3 si volume justifie.
•	Solution maison : table PostgreSQL `dataset_versions` avec hash, parent_version, timestamp, manifest JSON. Simple, sous contrôle total, mais réinvente la roue. Possible MVP V1 puis migration DVC en V2.
Décision recommandée : DVC dès la V1, avec convention claire : un dataset publié reçoit un tag immutable (ex: `pa6_grade_a@v1.2`), un modèle IA enregistre l'ID exact des datasets utilisés à l'entraînement.
8.8.4 Pipeline de Nettoyage et Validation
Tout dataset entrant — qu'il vienne d'une machine ou d'un upload utilisateur — passe par un pipeline de qualité en 5 étapes, exécuté en C++/Python selon la nature de l'opération :
  RAW DATA
      │
      ▼
  ┌─────────────────────────────────────────────────────┐
  │ ÉTAPE 1 — VALIDATION DE SCHÉMA                      │
  │  • Colonnes attendues présentes ?                   │
  │  • Types corrects (float, int, datetime) ?          │
  │  • Unités déclarées ?                               │
  │  → Rejet si schéma cassé                            │
  └────────────────────┬────────────────────────────────┘
                       ▼
  ┌─────────────────────────────────────────────────────┐
  │ ÉTAPE 2 — NORMALISATION DES UNITÉS                  │
  │  • Conversion vers SI (Pa, s, K)                    │
  │  • Détection automatique unités exotiques           │
  │  • Trace des conversions appliquées                 │
  └────────────────────┬────────────────────────────────┘
                       ▼
  ┌─────────────────────────────────────────────────────┐
  │ ÉTAPE 3 — DÉTECTION D'ANOMALIES                     │
  │  • Monotonie temporelle (t croissant)               │
  │  • Plages physiques (T > 0K, σ ≠ NaN)               │
  │  • Outliers statistiques (méthode IQR + isolation)  │
  │  • Trous (gaps temporels suspects)                  │
  │  → Avertissement utilisateur, pas rejet automatique │
  └────────────────────┬────────────────────────────────┘
                       ▼
  ┌─────────────────────────────────────────────────────┐
  │ ÉTAPE 4 — ENRICHISSEMENT METADATA                   │
  │  • Score qualité [0-1] calculé                      │
  │  • Hash SHA-256 du contenu                          │
  │  • Détection automatique du type d'expérience       │
  │  • Suggestion famille matériau (si non spécifiée)   │
  └────────────────────┬────────────────────────────────┘
                       ▼
  ┌─────────────────────────────────────────────────────┐
  │ ÉTAPE 5 — PERSISTANCE & INDEXATION                  │
  │  • Écriture Parquet + metadata.json dans MinIO      │
  │  • Indexation TimescaleDB (séries temporelles)      │
  │  • Indexation PostgreSQL (métadonnées recherche)    │
  │  • Notification user : prêt à utiliser              │
  └─────────────────────────────────────────────────────┘
8.8.5 Stockage
Stratégie de stockage en trois tiers, optimisée coût/performance :
Tier	Backend	Latence	Usage
Hot	Redis + PostgreSQL TimescaleDB	< 10 ms	Métadonnées actives, sondes des 30 derniers jours, sessions
Warm	MinIO / S3 standard tier	100 ms à 1 s	Datasets actifs, snapshots VTU des 90 derniers jours, modèles entraînés en cours d'usage
Cold	S3 Glacier / Glacier Deep Archive	Heures (avec restore)	Datasets archivés, snapshots > 1 an, audit trail compliance

Politique de migration automatique entre tiers : datasets non consultés depuis 90 jours basculent automatiquement Warm → Cold, sauf flag « keep hot » mis par l'utilisateur. Cette politique réduit le coût de stockage cloud de 60 à 80% sur les volumes accumulés.
8.8.6 Lien avec l'IA (Training & Calibration)
Les composants IA décrits en Partie 4 dépendent directement de cette infrastructure data. Cartographie explicite :
Composant IA	Données nécessaires	Pipeline d'entraînement
Auto-Fit IA (initialisation ML)	~2 000 campagnes étiquetées (modèle Prony optimal connu)	Train/val/test split 70/15/15, Gradient Boosting, validation k-fold, MLflow tracking, retrain trimestriel
Model Recommender	~5 000 paires (signature donnée → modèle gagnant)	Random Forest ou XGBoost, SHAP pour explicabilité, A/B test sur cas réels
TTSP Neural	~500 campagnes multi-températures avec shift factors connus	Réseau dense petite taille, comparaison contre WLF analytique, déploiement progressif (canari 5%)
Active Learning	Pas de jeu d'entraînement statique : modèle bayésien (GP) instancié par projet	Prior bayésien construit à partir des familles matériaux NIST, mise à jour live au fur et à mesure des essais

📊 Métriques de gouvernance data
Trois indicateurs clés à monitorer continuellement (dashboard Grafana dédié) :
① Volume sous gestion (TB) par tier et par tenant — pour anticiper les coûts cloud.
② Score qualité moyen des datasets — alerte si dégradation, signal d'un problème en amont.
③ Drift des modèles IA en production — KL-divergence entre distributions d'entrée train vs prod, déclenche un re-training si dépassement de seuil.
PARTIE 9 — Document Non Technique
Cette partie est destinée aux décideurs, investisseurs, partenaires commerciaux et utilisateurs non-techniques. Elle présente RheoSim Enterprise en évitant le jargon et en se concentrant sur la valeur, l'impact et la trajectoire.
9.1 Description Simple
RheoSim Enterprise est un logiciel en ligne qui aide les ingénieurs et chercheurs à comprendre comment les matériaux se comportent dans le temps.
Beaucoup de matériaux modernes — les plastiques, les caoutchoucs, les composites — ont une particularité : leur réponse à une force dépend non seulement de l'intensité de cette force, mais aussi de la durée pendant laquelle elle est appliquée. Un joint en caoutchouc comprimé pendant 10 ans ne réagit pas comme celui qui vient d'être installé. Une pièce plastique en aéronautique qui supporte sa charge pendant toute la durée du vol finit par se déformer progressivement.
Prédire ces comportements avec précision est essentiel dans l'aéronautique, l'automobile, le biomédical, l'emballage. Aujourd'hui, cette prédiction nécessite un patchwork d'outils coûteux et complexes, utilisés par une poignée d'experts. RheoSim change cela : un seul outil, accessible via un navigateur, qui couvre tout le processus, depuis les données brutes du laboratoire jusqu'au rapport final prêt à publier.
9.2 Les Bénéfices Concrets
Bénéfice 1 — Gain de temps massif
Ce qui prend aujourd'hui une semaine à un ingénieur qualifié peut être fait en une heure avec RheoSim. Non pas parce que le logiciel « fait le travail à la place de l'ingénieur », mais parce qu'il supprime toutes les étapes de transfert manuel d'information entre outils. L'ingénieur garde le contrôle — il prend juste ses décisions plus vite et sur des bases plus solides.
Bénéfice 2 — Qualité supérieure
Les méthodes traditionnelles d'identification produisent souvent des paramètres qui reproduisent les données expérimentales mais ne sont pas physiquement cohérents. RheoSim intègre des garde-fous physiques (positivité, ordres de grandeur, cohérence avec la famille matériau) qui garantissent des résultats interprétables et défendables.
Bénéfice 3 — Reproductibilité
Un problème récurrent en R&D : deux ingénieurs travaillant sur les mêmes données produisent des résultats différents. Avec RheoSim, chaque analyse est encapsulée dans un fichier unique (case.json) qui peut être partagé, archivé, et rejoué à l'identique. C'est un saut qualitatif pour la qualité et la traçabilité.
Bénéfice 4 — Accessibilité
Pas d'installation lourde, pas de licence à 30 000 € par poste, pas de serveur de calcul à administrer. Un navigateur, un compte, et on travaille. Cette accessibilité ouvre la caractérisation visco-élastique à des acteurs qui en étaient exclus par les barrières économiques : PME, startups matériaux, universités hors des métropoles, pays émergents.
Bénéfice 5 — Intelligence embarquée
Des fonctionnalités d'IA discrètes mais puissantes : le logiciel suggère le meilleur modèle pour vos données, accélère l'identification des paramètres par un facteur 5 à 10, et recommande quelles expériences supplémentaires réaliser pour améliorer la fiabilité du modèle. Cette IA est un assistant, pas un remplaçant.
9.3 Avantages Concurrentiels
Face à Abaqus / ANSYS	Face aux scripts maison	Face aux OEM rhéomètres
Pas de licence coûteuse, workflow unifié (leurs outils = solveurs seuls)	Logiciel professionnel, maintenu, testé — vs code non pérenne	Ouverture : pas enfermé dans un constructeur de machine
Identification paramétrique native (pas eux)	Interface utilisateur moderne — vs scripts	Couverture multi-matériaux, multi-modèles
Reproductibilité bit-exact garantie	Conforme aux standards ASTM/ISO	Capacité simulation 3D (les OEM font juste du post-traitement)
Export vers leurs outils : complément, pas remplacement	Collaboration d'équipe native	Bibliothèque matériaux partagée

9.4 Valeur Ajoutée par Typologie d'Utilisateur
Pour les grands groupes industriels
Un grand groupe aéronautique ou automobile dépense entre 2 et 5 millions d'euros par an en licences de simulation. RheoSim Enterprise propose un complément stratégique : pour moins de 10% de ce budget, ils obtiennent un outil spécialisé qui accélère leurs campagnes visco-élastiques, réduit leur dépendance à un éditeur unique, et leur permet d'internaliser des compétences aujourd'hui externalisées.
Impact mesurable : sur un projet typique de qualification d'un nouveau grade composite, économie estimée entre 150 k€ et 400 k€ sur 18 mois (réduction d'essais physiques + temps ingénieur économisé).
Pour les laboratoires de recherche
Un laboratoire universitaire de rhéologie type gère simultanément 3 à 8 thèses. Chaque doctorant passe aujourd'hui entre 20% et 40% de sa première année à construire ses propres outils de traitement. RheoSim libère ce temps pour la recherche elle-même. Bénéfice : publications plus nombreuses, doctorats soutenus plus rapidement, classement du laboratoire amélioré.
Pour les universités et écoles
L'enseignement de la rhéologie et de la mécanique des matériaux souffre d'un décalage entre la théorie enseignée et la pratique moderne des ingénieurs. RheoSim en mode pédagogique comble ce gap : les étudiants manipulent le même outil que celui utilisé en industrie, avec un accompagnement guidé. Les licences campus sont volontairement abordables (< 5 k€/an pour un département) pour lever la barrière budgétaire.
Pour les PME et startups matériaux
Une startup qui développe un nouveau bio-polymère n'a ni les moyens d'une licence Abaqus, ni l'expertise pour coder son propre solveur. Avec RheoSim en abonnement (estimation : 200 à 500 €/mois selon usage), elle accède à un niveau d'analyse scientifique digne d'un grand groupe, ce qui accélère son time-to-market et renforce sa crédibilité technique face aux investisseurs.
9.5 Impact Attendu
Impact scientifique
À 3 ans, RheoSim aura généré entre 30 et 50 publications peer-reviewed co-citant l'outil. La bibliothèque de matériaux ouverte sera devenue une ressource communautaire, citable avec DOI, utilisée comme base pour les benchmarks et les cours.
Impact industriel
À 5 ans, estimation : 50 à 100 entreprises clientes, économies cumulées pour ces entreprises chiffrables à plusieurs dizaines de millions d'euros. Positionnement comme alternative crédible européenne dans un marché actuellement dominé par les éditeurs américains.
Impact formation
À 5 ans : 20 à 30 universités européennes utilisant RheoSim en cours, soit 2 000 à 5 000 ingénieurs formés par an. Ces ingénieurs deviennent des prescripteurs naturels de l'outil dans leur carrière.
Impact environnemental
Effet indirect mais réel : en permettant de simuler plus efficacement la durabilité long-terme des matériaux, RheoSim contribue à réduire les surdimensionnements (économie de matière) et à mieux valider les matériaux bio-sourcés (qui ont souvent des comportements visco-élastiques plus marqués). Impact CO₂ chiffrable avec une méthodologie ACV dédiée à moyen terme.
9.6 Vision à 5 Ans
« En 2030, RheoSim Enterprise est la plateforme de référence européenne pour la caractérisation et la simulation visco-élastique. Cité dans 500+ publications, utilisé par 150+ entreprises, déployé dans 30+ universités — tout en restant fidèle à ses principes fondateurs : reproductibilité, rigueur scientifique et standards ouverts. »
— Vision RheoSim 2030
Cette vision n'est pas un positionnement marketing : c'est la conséquence naturelle de trois choix stratégiques tenus dans le temps — (1) priorité absolue à la qualité scientifique, (2) modèle hybride open-core qui construit la communauté, (3) intégration IA native et non postiche qui crée une différenciation durable.
 
9.7 Stratégie Go-To-Market Progressive
RheoSim Enterprise s'attaque à un marché conservateur (ingénierie matériaux), avec des cycles d'achat longs et un coût de switching élevé. Une stratégie commerciale frontale (« on lance, on vend ») a peu de chances de fonctionner. La stratégie retenue est progressive, en trois phases superposées qui réduisent le risque utilisateur étape par étape et capitalisent sur les effets de communauté et de réseau.
9.7.1 Phase 1 — Open Source & Communauté Scientifique (Mois 0-12)
Audience cible : chercheurs académiques en rhéologie et mécanique des polymères, doctorants, post-docs.
Proposition de valeur : un outil open source rigoureux, gratuit, qui leur évite de coder leur propre solveur. Citation académique facile (DOI), exports LaTeX prêts à publier.
Actions concrètes Phase 1
•	Publication du cœur sous Apache 2.0 sur GitHub dès la sortie V1, avec README professionnel, CI publique, badge couverture de tests.
•	Présence à 2-3 conférences clés la première année (ESR conference, Society of Rheology meeting, AERC) avec poster + démonstration live.
•	Blog technique mensuel : benchmarks comparatifs, tutoriels, deep-dives méthodologiques. Objectif : 1 000 visiteurs uniques/mois à 12 mois.
•	Pré-print arXiv décrivant la méthodologie (« RheoSim: an open-source platform for visco-elastic characterization »).
•	Discord ou Slack communautaire avec channels dédiés (general, models, troubleshooting, contributors).
•	Programme « Champion Researcher » : 5 chercheurs reconnus reçoivent un support personnalisé en échange d'un retour public et de citations.
Indicateurs de succès Phase 1
•	500+ étoiles GitHub à 12 mois.
•	100+ utilisateurs actifs mensuels.
•	3-5 publications académiques citant RheoSim.
•	10+ contributeurs externes (issues, PRs).
Risques Phase 1
•	Risque : adoption trop lente. Mitigation : focus sur 5 « champions researchers » pour amorcer la pompe.
•	Risque : forks non contrôlés divergents. Mitigation : gouvernance ouverte mais explicite (BDFL ou comité technique), CONTRIBUTING.md clair.

9.7.2 Phase 2 — Early Adopters R&D Industriels (Mois 12-24)
Audience cible : départements R&D matériaux d'industriels innovants (équipementiers automobile, aéronautique, biomédical, packaging avancé).
Proposition de valeur : plateforme commerciale (V2) avec fonctionnalités entreprise (collaboration, SSO, support, exports CAO), construite sur le cœur open source désormais validé par la communauté académique. Crédibilité scientifique acquise + workflow industriel optimisé.
Actions concrètes Phase 2
•	Identification de 3-5 « lighthouse customers » industriels, idéalement avec figures publiques (CTO, head of R&D) prêtes à témoigner publiquement.
•	Programme pilote 6 mois à tarif symbolique : implication client de 2 jours/mois feedback en échange d'un accès anticipé. Budget : 5 à 15 k€/an.
•	Études de cas (case studies) publiées avec les lighthouse customers : « Comment ACME a réduit de 80% son temps de caractérisation EPDM ».
•	Webinaires mensuels co-animés avec les early adopters : crédibilité par les pairs > marketing direct.
•	Présence à 2-3 salons industriels par an (JEC Composites, K Trade Fair, Salon de l'Aéronautique).
•	Lancement du modèle freemium : cœur open source gratuit ad vitam, fonctionnalités premium en abonnement (5 à 50 k€/an selon nombre de seats et modules).
•	Premier responsable commercial à mi-Phase 2 : profil Sales Engineer avec compétence rhéologie minimum.
Indicateurs de succès Phase 2
•	10-20 entreprises clientes payantes.
•	ARR > 200 k€.
•	3 case studies industriels publiés.
•	NPS clients > 40 (excellent en B2B SaaS).
Risques Phase 2
•	Risque : tension open source vs propriétaire mal communiquée → fork hostile par la communauté. Mitigation : politique transparente sur ce qui est core/premium, gouvernance respectée.
•	Risque : sales cycle plus long que prévu (12-18 mois pour un grand industriel vs 3-6 mois espérés). Mitigation : plan de trésorerie réaliste, ne pas surinvestir avant validation des premiers cycles.

9.7.3 Phase 3 — Plateforme Enterprise SaaS Référente (Mois 24-36+)
Audience cible : grands comptes industriels multi-sites internationaux + universités sur licences campus + écosystème de plugins développé par tiers.
Proposition de valeur : standard de facto européen pour la simulation visco-élastique, avec multi-tenant SaaS, déploiement on-premise pour les grands comptes sensibles, marketplace de plugins, intégrations CAO natives.
Actions concrètes Phase 3
•	Équipe commerciale élargie : Account Executives sectoriels (aéronautique, automobile, biomédical), Customer Success Managers, Solution Architects.
•	Marketplace de plugins ouverte avec partage de revenus (70/30 développeur/RheoSim) — incite des tiers à développer des modèles spécialisés.
•	Partenariats stratégiques avec les éditeurs CAO (intégrations Abaqus, ANSYS, NX, CATIA) — RheoSim devient le complément spécialisé visco-élastique de ces grandes plateformes.
•	Programme académique global : licences campus quasi-gratuites pour les 100 premières universités → 5 000 ingénieurs formés/an deviennent prescripteurs en 3-5 ans.
•	Audit SOC 2 Type II et certifications ISO 27001 → débloque les comptes les plus régulés (défense, biomédical).
•	Conférence utilisateurs annuelle (« RheoConf ») dès l'atteinte de 500 utilisateurs actifs — renforce la communauté et l'effet réseau.
Indicateurs de succès Phase 3
•	100+ entreprises clientes.
•	ARR > 1,5 M€, croissance > 80% YoY.
•	30+ universités sous licence campus.
•	10+ plugins tiers actifs sur la marketplace.
•	Break-even ou rentabilité opérationnelle atteinte.

9.7.4 Stratégies de Réduction du Risque Utilisateur
Trois mécanismes transverses aux trois phases pour abaisser la barrière à l'adoption :
•	« Land and expand » contrôlé : entrer chez un client par une équipe R&D non-critique, prouver la valeur sur un projet pilote, étendre par contagion. Ne jamais vendre frontalement contre un Abaqus en place.
•	Compatibilité préservée : RheoSim exporte vers Abaqus / ANSYS / OpenFOAM dès la V2. Le message marketing : « gardez vos solveurs existants, gagnez juste sur la phase de caractérisation ».
•	Reversibilité : toutes les données utilisateur sont exportables dans des formats ouverts (CSV, JSON, VTK). Aucun lock-in propriétaire — argument fort face aux DSI.
9.7.5 Effet de Réseau — La Bibliothèque de Matériaux
L'asymétrie compétitive durable de RheoSim ne vient pas du code (qu'un compétiteur peut recoder en 18 mois) mais des effets de réseau. Le mécanisme central est la bibliothèque de matériaux.
À chaque nouvelle utilisation publique, un matériau caractérisé est versionné, attribué à son contributeur, et rendu disponible (sous CC-BY) pour l'ensemble de la communauté. Au bout de 24 mois, la bibliothèque dépasse 1 000 matériaux indexés. À ce point, elle devient une ressource scientifique de référence — citée dans les publications, utilisée dans les cours, valorisée comme un standard. Aucun compétiteur ne peut la reconstituer rapidement : c'est une accumulation de capital communautaire.
Ce mécanisme est la traduction concrète de la stratégie open-core : on donne le code, on conserve la position de gardien d'un commun précieux (la bibliothèque). Plus la bibliothèque grandit, plus l'outil devient incontournable, plus la position commerciale est défendable.

🚀 Le pari sous-jacent
Cette stratégie suppose que RheoSim sache patienter en Phase 1 sans céder à la pression de monétisation rapide. C'est l'erreur classique des startups deep-tech : vouloir vendre avant d'avoir construit la légitimité. Trois ans patients valent mieux que trois ans de vente forcée qui brûlent la marque.

La rentabilité opérationnelle visée n'est atteinte qu'en milieu de Phase 3 (mois 30-36). C'est une trajectoire deep-tech classique, qui exige un actionnariat patient et une équipe dirigeante alignée sur cet horizon.
PARTIE 10 — Critique Experte
Cette partie finale adopte une posture critique sans concession. Tout projet ambitieux contient des angles morts et des fragilités. Les identifier tôt, sans complaisance, est ce qui différencie un projet exécutable d'un projet fantasmé.
10.1 Points Faibles Structurels du Projet
Point faible 1 — Ambition technique trop large
Le projet embrasse quatre domaines simultanément : modélisation physique avancée, solveurs numériques, IA appliquée, et architecture cloud distribuée. Chacun de ces domaines mobilise une expertise spécialisée. Peu d'équipes au monde réunissent ces quatre compétences à un haut niveau.
Risque : des compromis techniques dans certaines zones par manque d'expertise, notamment au croisement physique / IA où les subtilités (interprétabilité des recommandations, validité physique des prédictions) sont critiques.
Recommandation : recruter au moins une personnalité senior par domaine dès la phase V1. Prévoir des partenariats académiques pour les zones les plus expertes (identification paramétrique inverse, TTSP neural). Ne pas tenter de tout faire en interne.
Point faible 2 — Adoption utilisateur sous-estimée
Les ingénieurs matériaux sont parmi les utilisateurs logiciels les plus conservateurs. Leur outil actuel — même médiocre — est prouvé, validé par l'autorité de certification qui a accepté leurs derniers dossiers, et connu de leurs collègues. Changer d'outil représente un coût de switching massif : revalidation, formation, risque qualité.
Risque concret : même un outil objectivement supérieur peut mettre 3 à 5 ans à s'imposer, alors que le business plan suppose une adoption en 18 mois.
Recommandation : pas de pari frontal sur le remplacement. Positionnement en complément (export vers Abaqus/ANSYS) pour réduire le risque perçu. Stratégie de land-and-expand : entrer par les équipes R&D non-productives, puis se diffuser par contagion.
Point faible 3 — Modèle économique fragile en phase V1
Trois utilisateurs pilotes en V1 ne génèrent pas de revenu. Le développement V1 (6 mois, équipe de 4-5 personnes) coûte entre 300 k€ et 500 k€. Sans financement initial (subvention, business angel, seed) ou bootstrap par prestation de service, le projet risque l'épuisement de trésorerie avant même d'atteindre V2.
Recommandation : sécuriser un financement 24 mois AVANT de démarrer la V1. Options : (a) subvention BPI France type iLab ou équivalent H2020, (b) lever un seed round de 1-1,5 M€, (c) adosser le projet à une activité de prestation de conseil rhéologie qui finance le produit. Ne pas démarrer sans runway clair.
10.2 Risques Techniques Critiques
Risque	Manifestation probable	Mitigation concrète
Convergence solveur FEM 3D	Sur cas réel industriel complexe, Newton-Raphson diverge ou converge lentement	Benchmarking précoce contre Abaqus sur 5 cas NAFEMS, collaboration chercheur expert solveur, fallback sur solveur externe (Code_Aster) si V2 insuffisant
Identification non-robuste	Sur données expérimentales bruitées, paramètres Prony fantaisistes (valeurs négatives, τ aberrants)	Régularisation obligatoire par défaut, limites hardcodées par famille matériau, tests sur jeux de données publics (> 50 campagnes)
Performance C++ / JVM interop	gRPC entre Spring et C++ devient bottleneck sur petits jobs	Serveur C++ long-running (pas spawn par job), batching des appels, co-localisation réseau
Dérive des modèles IA	Le Model Recommender entraîné sur 2024 donne des recommandations absurdes sur matériaux 2027	Versioning strict des modèles IA, monitoring de drift, réentraînement trimestriel, canari sur 5% trafic
Qualité variable des parsers	Nouveau format DMA non supporté → utilisateur bloqué	Système de plugin parser, possibilité utilisateur de décrire son format en YAML, import fallback CSV
Sécurité données entreprise	Fuite de données matériaux confidentiels client	Chiffrement at-rest + in-transit, audit SOC2 en V2, option on-premise pour grands comptes

10.3 Erreurs à Éviter
Erreur 1 — Sur-engineering précoce
La tentation est grande, vu l'ambition V3, de commencer à coder « proprement pour plus tard » : microservices dès le jour 1, Kubernetes pour trois utilisateurs, architecture event-sourced ultra-découplée. C'est une trappe coûteuse : on consomme 60% du temps V1 en infrastructure au détriment des fonctionnalités produit.
Règle : V1 = monolithe Spring Boot + base PostgreSQL + un seul worker C++. Les microservices apparaissent en V2 quand la pression réelle les justifie.
Erreur 2 — Ignorer le design UI / UX
Les équipes dominées par les ingénieurs numériques produisent souvent des interfaces illisibles pour les utilisateurs finaux. Cette erreur est fatale dans un marché où l'utilisateur cible compare inconsciemment à Notion, Figma ou Linear — pas à ANSYS 2005.
Règle : un designer UI/UX (profil produit, pas décoratif) dès la V1, au même niveau que les ingénieurs, avec droit de veto sur toute interface.
Erreur 3 — Négliger la documentation et la formation
Un logiciel scientifique sans tutoriels, vidéos, et documentation méthodologique rigoureuse est un logiciel qui ne se vend pas. La documentation n'est pas un extra : c'est un livrable de premier ordre.
Règle : 10% du temps de développement V1 consacré à la documentation, avec un responsable dédié (technical writer à temps partiel dès le mois 3).
Erreur 4 — Viser trop large en personas
Tenter de plaire aux chercheurs (qui veulent flexibilité maximale), aux industriels (qui veulent validité certifiée) et aux étudiants (qui veulent simplicité) avec UNE interface unique conduit à une interface médiocre pour tous.
Règle : en V1, prioriser UN persona (recommandé : Élise, ingénieur R&D industriel). V2 ajoute un mode avancé pour la persona chercheur. V3 ajoute le mode pédagogique. Ne pas tout faire en même temps.
Erreur 5 — Sous-estimer la validation scientifique
La crédibilité scientifique de RheoSim sera scrutée. Un seul benchmark raté, un cas divergent public, et la réputation est à reconstruire pendant 2 ans.
Règle : processus de validation scientifique rigoureux, chaque release majeure passe 50+ cas de validation, résultats publiés en open access, politique zéro-régression scientifique avec CI bloquante.
10.4 Recommandations Stratégiques
Recommandation 1 — Adopter une posture open-core assumée
Le cœur physique (modèles, solveurs 1D, identification basique) doit être open-source sous Apache 2.0. Cela construit la crédibilité scientifique, attire les contributeurs, et crée l'écosystème enseignement gratuitement. Les modules premium (IA avancée, SSO, support, collaboration temps réel, intégrations CAO) sont propriétaires. Ce modèle a fait ses preuves (GitLab, Elastic avant leur virage, MongoDB).
Recommandation 2 — S'adosser à un institut de recherche
Un partenariat formel avec un laboratoire de rhéologie reconnu (par exemple : Navier à l'ENPC, IMSIA à Saclay, CEMEF à Mines ParisTech, DESMAT à Strasbourg, ou équivalents européens type TU Eindhoven, ETH Zürich) apporte trois choses : (1) légitimité scientifique, (2) données expérimentales pour validation, (3) accès à des doctorants top niveau pour les extensions avancées.
Recommandation 3 — Construire la communauté avant le produit
Avant même la V1, lancer : un blog technique avec contenu à forte valeur ajoutée (benchmarks, comparaison modèles, tutoriels open source), une newsletter mensuelle, une présence sur arXiv (pré-prints méthodologiques), et un serveur Discord / Slack communautaire. Quand V1 sort, on a déjà 500 à 1000 personnes intéressées.
Recommandation 4 — Définir des OKR trimestriels publics
Des objectifs mesurables, transparents, partagés avec toute l'équipe. Un OKR raté est une information précieuse. Un OKR atteint facilement signale un manque d'ambition. Cette discipline, inspirée des cultures Google / Intel, évite la dérive et les projets zombie.
Recommandation 5 — Préparer la stratégie de sortie dès V1
Sans définir la sortie comme finalité, anticiper les scénarios : acquisition par un grand éditeur (Ansys, Dassault, Altair, Hexagon), acquisition par un industriel utilisateur (Safran, Michelin, Airbus), IPO, croissance organique indépendante. Chaque scénario a des implications différentes sur la gouvernance et la structure capitalistique — mieux vaut y réfléchir à froid en V1 qu'en urgence en V3.

🎯 Synthèse critique
RheoSim Enterprise est un projet de grande qualité intellectuelle, portant sur un vrai problème, avec une vision claire et des innovations défendables. Ses risques principaux ne sont pas techniques mais stratégiques et organisationnels : ambition trop large, adoption lente, financement fragile en phase amorçage.

Avec une exécution disciplinée — focus V1 MVP, financement 24 mois sécurisé, partenariat académique, designer UX dès le jour 1 — le projet a une fenêtre de succès réelle. Sans cette discipline, il rejoindra la longue liste des simulateurs scientifiques prometteurs mais jamais industrialisés.
10.5 Feu Vert Conditionnel
Ma recommandation finale, en tant qu'expert externe, est un GO conditionnel. Le projet mérite d'être lancé, mais sous trois conditions cumulatives :
28.	Financement sécurisé 24 mois minimum AVANT le premier commit de code V1 (750 k€ à 1,5 M€ selon taille d'équipe).
29.	Équipe fondatrice complète : un CTO/tech-lead senior C++ et architecture, un lead scientifique rhéologie (niveau Dr ou senior industrie), un product/UX, un développeur fullstack senior. Quatre profils non-substituables.
30.	Trois utilisateurs pilotes engagés : lettres d'intention signées, prêts à payer symboliquement la V1, et à donner 2 jours/mois de feedback. Sans ce signal marché, le projet reste une hypothèse.
Si ces trois conditions sont remplies, le projet a une probabilité de succès estimée entre 25 et 40 % — ce qui est élevé pour un projet deep-tech en phase amorçage. Si une seule de ces conditions manque, la probabilité tombe en dessous de 10 %, et le projet est prématuré.

« Un bon projet mal financé et mal équipé est un mauvais projet. Un projet moyen correctement financé et bien équipé peut devenir excellent. La qualité de l'exécution domine statistiquement la qualité de l'idée initiale. »
— Principe d'exécution

