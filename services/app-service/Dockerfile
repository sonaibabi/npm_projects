# ---------- build stage ----------
FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm ci --omit=dev

COPY app.js .

# ---------- runtime stage ----------
FROM node:20-alpine

WORKDIR /app

RUN addgroup -S nodejs && adduser -S nodejs -G nodejs
USER nodejs

COPY --from=builder /app ./

EXPOSE 3000
CMD ["node", "app.js"]
