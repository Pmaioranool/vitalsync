# === POURQUOI UTILISER LE MULTI-STAGE BUILD ? ===
# Le multi-stage build est pertinent pour deux raisons majeures :
# 1. Sécurité : Il réduit la surface d'attaque en excluant l'outillage de développement
# 2. Taille d'image : En ne conservant que l'environnement métier strict l'image finale est
#    considérablement allégée, ce qui rend les déploiements plus rapides et moins coûteux.



FROM node:20-alpine AS builder

WORKDIR /app

# Copie des fichiers décrivant les dépendances
COPY package*.json ./

# Installation de TOUTES les dépendances (dont celles de dev pour les tests)
RUN npm install

# Copie du code source complet (y compris le dossier de test)
COPY . .

# Exécution des tests. Si cette commande échoue, l'image finale ne sera jamais créée.
RUN npm test

FROM node:20-alpine AS production

WORKDIR /app

# Définition de l'environnement en production
ENV NODE_ENV=$

COPY package*.json ./

# Installation UNIQUEMENT des dépendances nécessaires
RUN npm install --omit=dev

COPY --from=builder /app/server.js ./

# Exposition du port d'écoute de l'application
EXPOSE 3000

# Commande de démarrage du serveur
CMD ["node", "server.js"]
