# Install Dependencies
FROM node:21.4-slim AS dependencies
WORKDIR /app
COPY package*.json ./
RUN npm install -f
RUN npm install sharp -f

# Build
FROM dependencies AS builder
WORKDIR /app
COPY . .
RUN npm run build


# run the app using npm start
FROM node:21.4-slim AS runner
WORKDIR /app
COPY . .
COPY --from=dependencies /app/node_modules ./node_modules
EXPOSE 3002
CMD ["npm", "start", "--", "--port", "3002"]
