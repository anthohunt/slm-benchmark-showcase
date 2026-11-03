> Showcase repository: the code and data of this project are private; this README describes it. / Dépôt vitrine : le code et les données de ce projet sont privés ; ce README le décrit.

# Small model evaluation bench

A web bench that puts the same set of 28 questions to small language models (SLMs) and scores their answers without a human or LLM judge.

## The problem

Choosing a small model for an on-device agent (virtual reality headset, smartphone) requires knowing what it actually gets right, with which instructions and within which memory. The bench was built for a supervised internship at an engineering school: the student runs series and reads the results on their own.

## How it works

- Three settings: the model, the target hardware (Quest 3 headset, 8 or 12 GB smartphone, 16 GB laptop, 32 GB workstation, server) and the system prompt. The hardware sets the context size; devices the model does not fit on are removed.
- 28 questions in three families: 5 performance indicator trees, 6 causal chains, 17 multiple-choice questions on a course, with retrieval from that course (RAG).
- Each answer is validated against a schema, then scored by deterministic rules: tree or chain structure, allowed transitions between node types, exact letter for multiple-choice questions.
- The main score is the number of fully correct questions; alongside it, first-attempt successes and the average of rules passed.
- Each question expands: failed checks, raw answer, 3D graph of the model's answer next to a reference answer.

## What is built

Running continuously on the institution's internal network.

- Three models available: Gemma 4 26B, Gemma 4 8B and LFM2.5-1.2B, the target small model.
- System prompts saved as versions per family; a prompt modified without being saved is flagged and marked in the history.
- Run history and a curve that only links comparable runs.
- Check before handover: 6 combinations out of 6 with no technical error. Time per question: 120 to 175 s for the 26B, 40 to 57 s for the 8B, 14 s for LFM2.5.
- Models run on CPU: measured latencies say nothing about a GPU or a headset.
- Not done yet: archiving the exact prompt text with each run, repeating a question to measure variance, keeping raw output from complete failures.

## What is public

This showcase is public; the code, questions and results remain private, in the institution's repository.

## Tech stack

- Python, uv
- Ollama, pydantic-ai and Pydantic for structured outputs
- LangChain, Chroma and nomic-embed-text for course retrieval
- Three.js for 3D graphs
- Docker Compose

---

## Version française

# Banc d'évaluation de petits modèles

Un banc web qui fait passer à des petits modèles de langage (SLM) une même série de 28 questions et note leurs réponses sans juge humain ni LLM-juge.

## Le problème

Choisir un petit modèle pour un agent embarqué (casque de réalité virtuelle, smartphone) demande de savoir ce qu'il réussit vraiment, avec quelle consigne et dans quelle mémoire. Le banc a été construit pour un stage encadré dans une école d'ingénieurs : l'étudiant y lance ses séries et lit les résultats seul.

## Comment ça marche

- Trois réglages : le modèle, le matériel visé (casque Quest 3, smartphone 8 ou 12 Go, portable 16 Go, poste 32 Go, serveur) et le prompt système. Le matériel fixe la taille de contexte ; les appareils où le modèle ne tient pas sont retirés.
- 28 questions en trois familles : 5 arbres d'indicateurs de performance, 6 chaînes causales, 17 QCM posés sur un cours, avec recherche dans ce cours (RAG).
- Chaque réponse est validée contre un schéma, puis notée par des règles déterministes : structure de l'arbre ou de la chaîne, transitions autorisées entre types de nœuds, lettre exacte pour les QCM.
- Le score principal est le nombre de questions entièrement correctes ; à côté, les réussites du premier coup et la moyenne des règles passées.
- Chaque question se déplie : vérifications échouées, réponse reçue, graphe 3D de la réponse du modèle face à une réponse de référence.

## Ce qui est construit

En service en continu sur le réseau interne de l'établissement.

- Trois modèles disponibles : Gemma 4 26B, Gemma 4 8B et LFM2.5-1.2B, le petit modèle visé.
- Prompts système enregistrés en versions par famille ; un prompt modifié sans être enregistré est signalé et marqué dans l'historique.
- Historique des séries et courbe qui ne relie que des séries comparables.
- Vérification avant remise : 6 combinaisons sur 6 sans erreur technique. Durée par question : 120 à 175 s pour le 26B, 40 à 57 s pour le 8B, 14 s pour LFM2.5.
- Les modèles tournent sur processeur : les latences mesurées ne disent rien d'un GPU ni d'un casque.
- Pas encore fait : archiver le texte exact du prompt avec chaque série, répéter une question pour mesurer la variance, garder la sortie brute des échecs complets.

## Ce qui est public

Cette vitrine est publique ; le code, les questions et les résultats restent privés, dans le dépôt de l'établissement.

## Pile technique

- Python, uv
- Ollama, pydantic-ai et Pydantic pour les sorties structurées
- LangChain, Chroma et nomic-embed-text pour la recherche dans le cours
- Three.js pour les graphes 3D
- Docker Compose
