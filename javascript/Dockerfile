FROM node:20-alpine AS builder

WORKDIR /app

COPY package.json ./
COPY package-lock.json ./

RUN npm install --only=production

COPY . .

FROM node:20-alpine

WORKDIR /app

COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/app.js .
COPY --from=builder /app/package.json .

EXPOSE 3000

CMD ["npm", "start"]
