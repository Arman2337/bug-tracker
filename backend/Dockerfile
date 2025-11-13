# server/Dockerfile
FROM node:18-alpine

# create non-root user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
WORKDIR /usr/src/app

# install deps
COPY backend/package*.json ./
RUN npm ci --only=production

# copy source
COPY backend/ . 

# if build step required (eg. TypeScript)
# RUN npm run build

# environment
ENV NODE_ENV=production
# expose port your server uses (commonly 5000 or 4000)
EXPOSE 5000

# use non-root user
USER appuser

# start
CMD ["node", "server.js"]
# or if project uses start script in package.json:
# CMD ["npm", "start"]

