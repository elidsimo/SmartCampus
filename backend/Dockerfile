# ---------- Étape 1 : compiler le TypeScript ----------
FROM node:22-alpine AS build
WORKDIR /app

# Toutes les dépendances (y compris typescript), pour compiler
COPY package.json package-lock.json ./
RUN npm ci

COPY tsconfig.json ./
COPY src ./src
RUN npm run build

# ---------- Étape 2 : image finale d'exécution ----------
FROM node:22-alpine
WORKDIR /app

ENV NODE_ENV=production
ENV PORT=8080

# Seulement les dépendances de production
COPY package.json package-lock.json ./
RUN npm ci --omit=dev && npm cache clean --force

# On récupère uniquement le code compilé de l'étape 1
COPY --from=build /app/dist ./dist

EXPOSE 8080
USER node
ENTRYPOINT ["node", "dist/index.js"]
