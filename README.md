# BinanceBot MicroServices — Architecture distribuée (NodeJS + Python + Docker)

**BinanceBot MicroServices** est une architecture distribuée conçue pour orchestrer un ensemble de microservices autour d’un bot interagissant avec l’API Binance.

L’objectif du projet est d’explorer la conception d’un **système backend modulaire**, composé de services autonomes, conteneurisés via Docker, et communiquant entre eux par API.  
Un seul composant — le **bot de trading** — est écrit en **Python**, tandis que **l’ensemble des autres microservices sont en JavaScript (Node.js)**.

⚠️ **Ce projet est un prototype d’exploration technique**, pas un bot destiné au trading réel.

---

## 🎯 Objectifs du projet

- Concevoir une **architecture microservices complète**  
- Isoler chaque fonctionnalité dans un service indépendant (Node.js)  
- Intégrer un bot de trading Python dans un système orchestré  
- Utiliser **Docker + docker-compose** pour gérer toute l’infrastructure  
- Simuler un environnement proche d’un backend professionnel  
- Établir une communication claire entre services : API REST, appels inter-services  
- Comprendre les bonnes pratiques de modularité, scalabilité et isolation

Ce projet démontre ma capacité à réfléchir en termes **d’architecture**, pas seulement de code.

---

## 🧱 Architecture technique

### 🟦 Services en NodeJS (JavaScript)

#### **API Gateway**
- Point d’entrée unique  
- Route les requêtes vers les autres services  
- Assure la validation et la cohérence des réponses  

#### **Service d’authentification**
- Gestion des utilisateurs  
- Hash des mots de passe  
- Génération / validation de tokens  
- Sessions & autorisations

#### **Service “Binance API” (wrapper JS)**
- Interagit avec l’API Binance (fetch, endpoints, sécurité)  
- Fournit au bot des données prêtes à l’emploi  
- Évite de mélanger logique de trading et API externes  

#### **Service de gestion (logs, statistiques, ou back-office selon ton repo)**
- Traite les informations venant du bot ou du gateway  
- Centralise des données utiles au monitoring

---

### 🟨 Service Python : **Bot de trading**
- Script Python dédié au bot  
- Appelle le service “Binance API” (Node)  
- Implémente la stratégie / logique du bot  
- Peut être exécuté en isolé dans un conteneur  
- Conçu pour être facilement remplaçable ou amélioré

---

### 🐳 Docker & Orchestration

Toute l’architecture fonctionne via `docker-compose` :

- chaque service est un conteneur  
- isolation complète  
- reproductibilité  
- environnement cohérent  
- démarrage simple d’un seul coup
