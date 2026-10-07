# Rapport Technique : Mon projet DevSecOps E-Commerce

## 1. Introduction
Pour cet examen, j'ai mis en place une application e-commerce simple qui se connecte à l'API publique DummyJSON. Le but est de montrer comment on développe, conteneurise, sécurise et déploie une application moderne en suivant les bonnes pratiques DevOps et DevSecOps.

---

## 2. Mes choix techniques (et pourquoi je les ai pris)

| Ce qu'on demande | Mon choix | Pourquoi j'ai choisi ça | L'autre choix que j'ai laissé tomber |
| :--- | :--- | :--- | :--- |
| **Code Source** | GitHub + branche `main` | C'est simple, rapide, tout le monde connaît et ça évite de se compliquer la vie. | GitFlow (trop lourd pour un projet solo). |
| **CI/CD** | GitHub Actions | C'est gratuit, c'est directement dans GitHub et ça s'exécute tout seul à chaque push. | Jenkins (il faut installer un serveur, trop de galère). |
| **Conteneur** | Docker (Nginx Alpine) | L'image est ultra légère, ça tourne partout pareil, zéro prise de tête. | Une machine virtuelle (trop lourd et lent). |
| **Sécurité** | Trivy | C'est gratuit, rapide, ça scanne le code et les images Docker pour trouver les failles. | Snyk (souvent payant ou limité). |
| **Infrastructure** | Kubernetes (Manifests YAML) | C'est ce qui est demandé pour la gestion des conteneurs en prod et la scalabilité. | Docker Compose (un peu trop basique). |

---

## 3. Comment fonctionne l'application ?
- **Côté utilisateur :** On arrive sur la page web, on peut se connecter avec les identifiants de test (`POST /auth/login`), chercher des produits, filtrer par catégorie et ajouter des articles dans le panier (`/carts`).
- **Côté CI/CD :** Dès que je pousse mon code sur GitHub, l'action GitHub lance un scan de sécurité avec Trivy pour vérifier qu'il n'y a pas de grosse faille, puis il construit l'image Docker.

---

## 4. Sécurité
- Je n'ai mis aucun mot de passe ou clé en clair dans le code.
- Le scanner Trivy bloque le pipeline si une faille grave est détectée.

---

## 5. Conclusion
Ce projet m'a permis de regrouper le front-end, Docker, la sécurité automatisée avec le pipeline et Kubernetes. C'est une base propre, fonctionnelle et prête pour l'évaluation.