# Stage 1: Install dependencies
FROM node:18 AS dependencies
WORKDIR /app

# Install pnpm globally
RUN npm install -g pnpm

# Copy only the necessary files for installing dependencies
COPY package.json pnpm-lock.yaml ./

# Install dependencies
RUN pnpm install --frozen-lockfile

# Copy the rest of the project files
COPY . .

# Build the project
RUN pnpm run build

# Stage 2: Production image
FROM node:18 AS runner
WORKDIR /app

RUN npm install -g pnpm


# Copy over the node_modules and .next directory from the previous stage
COPY --from=dependencies /app/node_modules ./node_modules
COPY --from=dependencies /app/.next ./.next
COPY --from=dependencies /app/public ./public
COPY --from=dependencies /app/package.json ./package.json

# Expose port and set environment
EXPOSE 3000
ENV PORT 3000
ENV NODE_ENV production

# Start the application
CMD ["pnpm", "start"]

