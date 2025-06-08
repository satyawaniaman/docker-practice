FROM node:18-alpine

# Set working directory
WORKDIR /app

# Install pnpm
RUN npm install -g pnpm

# Copy project files
COPY . .

# Install dependencies
RUN pnpm install


EXPOSE 3000

CMD ["node", "index.js"]
