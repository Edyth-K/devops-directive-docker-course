FROM node:19.6-alpine
# good practice to define working dir instead of just in root
WORKDIR /usr/src/app
# node looks for environment variables
ENV NODE_ENV production

COPY package*.json ./
# CI = clean install; dont install dev dependencies
# mount cache location to raise build speed
RUN --mount=type=cache,target=/usr/src/app/.npm \
    npm set cache /usr/src/app/.npm && \
    npm ci --only=production
# for security, use non root user within container
USER node

COPY --chown=node:node ./src .
# this is just documentation for users so they know it's on port 3000
EXPOSE 3000

CMD ["node", "index.js"]