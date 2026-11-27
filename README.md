Knowledge Assistant RAG

Assistant intelligent de gestion et d'exploitation des connaissances d'entreprise

1. Présentation du projet

Knowledge Assistant RAG est un projet de développement d'un assistant intelligent destiné à faciliter l'accès aux connaissances internes d'une entreprise.

Basé sur une architecture Retrieval-Augmented Generation (RAG), cet assistant permettra d'interroger une base documentaire interne et de générer des réponses contextualisées à partir des informations extraites des documents de référence.

Le premier cas d'usage concerne le support informatique : systèmes Linux et Windows, réseaux, infrastructures IT, procédures techniques et résolution d'incidents.

2. Problématique métier

Dans les entreprises, les équipes informatiques doivent régulièrement rechercher des informations dans différentes sources documentaires pour résoudre des incidents et répondre aux demandes des utilisateurs.

Cette recherche peut être longue, dispersée et dépendante de l'expérience des collaborateurs.

Le projet vise à centraliser ces connaissances et à faciliter leur exploitation grâce à l'intelligence artificielle générative.

3. Objectifs du projet

Centraliser la documentation technique et les connaissances internes.

Faciliter la recherche d'informations et la résolution des incidents IT.

Réduire le temps consacré à la recherche documentaire.

Générer des réponses contextualisées à partir des documents internes.

Fournir les références des documents utilisés pour justifier les réponses.

Concevoir une architecture évolutive et maintenable.

4. Architecture fonctionnelle cible

L'architecture RAG envisagée repose sur deux processus complémentaires.

4.1. Pipeline d'ingestion documentaire

    Collecte et chargement des documents.

    Extraction et nettoyage du contenu textuel.

    Découpage des documents en segments (chunking).

    Génération des représentations vectorielles (embeddings).

    Stockage des vecteurs et métadonnées dans une base vectorielle.

4.2. Pipeline de recherche et de génération

    Réception de la question utilisateur.

    Transformation de la question en embedding.

    Recherche des passages documentaires pertinents.

    Construction du contexte à transmettre au LLM.

    Génération d'une réponse contextualisée.

    Présentation de la réponse avec les sources documentaires.

5. Phases de développement et jalons

Le projet est organisé en plusieurs phases progressives. Chaque milestone correspond à un objectif technique et à des livrables identifiables.

Jalon	 Objectif	Livrable (critère de fin)
M0. Cadrage (2-3 jours)	Choisir le cas d'usage et les données	Un README avec le problème, le corpus (au moins 30 à 50 documents), 3 utilisateurs types et 20 questions réelles que le système doit savoir traiter
M1. Ingestion	Charger, nettoyer et découper les documents	Un script reproductible qui produit des chunks avec métadonnées (source, page, date). Un test unitaire sur le découpage
M2. Indexation et recherche	Embeddings, base vectorielle, recherche	Une fonction de recherche qui renvoie les top-k passages avec leur score. Vous pouvez expliquer pourquoi tel chunk est remonté
M3. Génération avec citations	Prompt, appel LLM, réponse sourcée	Réponses qui citent leurs sources et disent « je ne sais pas » quand le contexte manque
M4. API FastAPI	Exposer le système	Endpoints d'ingestion et de requête, schémas Pydantic typés, gestion d'erreurs, streaming si possible
M5. Évaluation	Mesurer au lieu de deviner	Un jeu de test de 30 à 50 questions avec réponses attendues, des métriques de retrieval (le bon passage est-il dans le top-k ?) et de fidélité, un rapport avant/après chaque changement
M6. Qualité et sécurité	Tests, robustesse, risques	Tests automatisés, protection contre l'injection de prompt dans les documents, secrets hors du code, limites de coût et de taille
M7. Observabilité et déploiement	Production	Logs structurés, traces des appels LLM, suivi des coûts et de la latence, Docker, CI/CD, déploiement sur AWS
M8. Documentation	Portfolio	README GitHub avec schéma d'architecture, décisions techniques et compromis, démo en ligne, résultats de l'évaluation



6. Stack technologique prévisionnel

Les technologies suivantes sont envisagées pour la réalisation du projet.
langage : Python 3.12 
orchestration : LangChain 
embeddings : Sentences Transformers  
Base vectoriel: Qdrant  
 LLM Local : Ollam QWEN  
 Backend : FastAPI  Frontend : Streamlit 
 Tests : Pytest  versionning : Git GitHub   
 conteneurisation : Docker   CI/CD GitHub actions 

7. Structure du projet

Le projet adopte une organisation Python basée sur le répertoire src/, afin de séparer le code applicatif des tests et de la configuration.

knowledge-assistant-rag/
├── src/
│   └── knowledge_assistant_rag/
│       ├── __init__.py
│       ├── config.py
│       └── schema.py
├── tests/
│   └── test_smoke.py
├── .gitignore
├── pyproject.toml
├── uv.lock
└── README.md

8.État d'avancement

Statut : En cours de développement.

Phase actuelle : M0 — Initialisation du projet.

Les travaux portent actuellement sur la configuration de l'environnement Python, la structuration du code source, la gestion des dépendances, les outils de qualité et le versionnement Git.

Les fonctionnalités du moteur RAG seront développées progressivement au cours des prochaines phases.