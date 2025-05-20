# syntax=docker/dockerfile:1
ARG NODE_VERSION=22.13.1
FROM node:${NODE_VERSION}-slim AS base
WORKDIR /app

# Install dependencies using npm ci for deterministic builds
COPY --link package.json ./
# No package-lock.json present, so fallback to npm install
RUN --mount=type=cache,target=/root/.npm \
    npm install --production

# Copy application files (excluding unwanted files via .dockerignore)
COPY --link . .

# Create a non-root user and switch to it
RUN addgroup --system mokepon && adduser --system --ingroup mokepon mokepon
USER mokepon

ENV NODE_ENV=production
ENV NODE_OPTIONS="--max-old-space-size=4096"

# Expose port if your app listens (not strictly needed for static or CLI)
# EXPOSE 3000

CMD ["node", "index.js"]
