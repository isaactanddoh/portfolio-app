# Build stage
FROM node:20-alpine AS builder

# Set working directory
WORKDIR /usr/src/app

# Copy package files first for better caching
COPY package*.json ./

# Remove package-lock.json
RUN rm -f package-lock.json

# Install dependencies with exact versions and clean npm cache
RUN npm install && \
    npm cache clean --force

# Copy application code
COPY . .

# Production stage
FROM node:20-alpine AS production

# Install dumb-init for proper process handling
RUN apk add --no-cache dumb-init && \
    addgroup -S nodejs && \
    adduser -S nodejsuser -G nodejs

# Set working directory
WORKDIR /usr/src/app

# Copy only necessary files from builder stage
COPY --from=builder --chown=nodejsuser:nodejs /usr/src/app/package*.json ./
COPY --from=builder --chown=nodejsuser:nodejs /usr/src/app/src ./src
COPY --from=builder --chown=nodejsuser:nodejs /usr/src/app/public ./public

# Install only production dependencies
RUN npm ci --only=production && \
    npm cache clean --force && \
    # Set strict permissions
    chmod -R 555 /usr/src/app && \
    chmod -R 444 /usr/src/app/node_modules && \
    # Create directory for temporary files if needed
    mkdir -p /usr/src/app/tmp && \
    chown -R nodejsuser:nodejs /usr/src/app/tmp && \
    chmod 755 /usr/src/app/tmp

# Set secure environment defaults
ENV NODE_ENV=production \
    PORT=3000 \
    NPM_CONFIG_AUDIT=true \
    NPM_CONFIG_AUDIT_LEVEL=high \
    NPM_CONFIG_FUND=false \
    NPM_CONFIG_STRICT_SSL=true \
    NODE_OPTIONS="--max-old-space-size=256 --max-http-header-size=8192" \
    # Disable Node.js process.env.NODE_TLS_REJECT_UNAUTHORIZED
    NODE_TLS_REJECT_UNAUTHORIZED=1

# Switch to non-root user
USER nodejsuser

# Expose port
EXPOSE 3000

# Use dumb-init as entrypoint
ENTRYPOINT ["/usr/bin/dumb-init", "--"]

# Start the application
CMD ["node", "src/app.js"]