[English](README.md) · **Français**

> Dépôt vitrine : le code et les données de ce projet sont privés ; ce README le décrit.

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
