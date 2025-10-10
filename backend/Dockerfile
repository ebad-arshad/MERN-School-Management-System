FROM node:24-alpine AS builder

WORKDIR /app

COPY ./package*.json /app/

RUN npm ci

COPY . .

EXPOSE 5000

CMD ["node", "index.js"]