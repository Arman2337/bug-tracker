# client/Dockerfile (multi-stage)
######## Build stage ########
FROM node:18-alpine AS builder
WORKDIR /app
ENV PATH /app/node_modules/.bin:$PATH

# copy package files first for better caching
COPY frontend/package*.json ./ 
# if using pnpm/yarn, adjust accordingly
RUN npm ci --silent

COPY frontend/ . 
# build for production (Vite: npm run build)
RUN npm run build

######## Production stage (nginx) ########
FROM nginx:stable-alpine AS production
# remove default nginx static (optional)
RUN rm -rf /usr/share/nginx/html/*

COPY --from=builder /app/build /usr/share/nginx/html

# copy custom nginx config if needed (optional)
# COPY client/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]


