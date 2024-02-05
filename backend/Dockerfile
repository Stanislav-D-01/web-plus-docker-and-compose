FROM node:16-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --no-audit
COPY . .
RUN npm run build

FROM node:16-alpine as production
WORKDIR /app
COPY package*.json ./
RUN npm ci --no-audit --omit=dev && npm i -g pm2
COPY --from=builder /app/dist ./dist
COPY ./ecosystem.config.js ./
#COPY ./.env ./
CMD ["pm2-runtime", "start", "ecosystem.config.js"]

