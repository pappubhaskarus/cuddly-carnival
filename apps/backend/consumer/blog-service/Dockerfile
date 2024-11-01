# Base image
FROM node:18

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json pnpm-lock.yaml ./
RUN npm install -g pnpm && pnpm install

# Bundle app source
COPY . .

# Build the app
RUN pnpm run build

# Start the app
CMD ["node", "dist/main"]
