# Image de base : Node 22 léger (Alpine)
FROM node:22-alpine

# Dossier de travail dans le conteneur
WORKDIR /app

# 1) Dépendances de production (couche mise en cache tant que package-lock.json ne change pas)
COPY package.json package-lock.json ./
RUN npm ci --omit=dev

# 2) Le code compilé (sortie de "npm run build", équivalent du JAR)
COPY dist ./dist

# Port d'écoute de l'API dans le conteneur
ENV NODE_ENV=production
ENV PORT=8080
EXPOSE 8080

# Ne pas exécuter l'application en root
USER node

# Commande lancée au démarrage du conteneur
ENTRYPOINT ["node", "dist/index.js"]
