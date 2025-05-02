# ─── Build stage ───
FROM node:18 AS builder
WORKDIR /usr/src/app

COPY ./package*.json ./
RUN npm install

COPY . .
COPY ./.husky .
RUN npm run build

# ─── Runtime stage ───
FROM node:18
WORKDIR /usr/src/app

# Install static server
RUN npm install -g serve

# Copy built files
COPY --from=builder /usr/src/app/build ./build

EXPOSE 3000
# run serve
CMD ["serve","-s","build","-l","3000"]
