FROM node:16-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --no-audit
COPY . ./
RUN npm run build

FROM nginx:latest as production
WORKDIR /app
COPY --from=builder /app/build /usr/share/nginx/html
COPY ./nginx/default.conf /etc/nginx/conf.d

CMD ["nginx", "-g", "daemon off;"]

