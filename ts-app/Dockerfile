FROM node:18-alpine as base

#stage 1
FROM base as builder

WORKDIR /app/build

COPY package.json .
COPY . .

RUN npm install
RUN npm run build

#stage 2
FROM base as runner
WORKDIR /app

COPY --from=builder /app/build/dist dist/
COPY --from=builder /app/build/package*.json ./

RUN npm install --omit=dev

# Expose the port the app runs on
EXPOSE 3000

# Command to run the app
CMD ["npm", "start"] 