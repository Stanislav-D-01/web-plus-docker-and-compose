FROM node:16-alpine AS builder
WORKDIR /app
COPY *.json ./
RUN npm i
COPY . .
RUN npm run build

FROM node:16-alpine as production
WORKDIR /app
COPY --from=builder /app/*.json ./
RUN npm i
COPY --from=builder ./app/dist ./dist
CMD ["npm","run", "start"]

