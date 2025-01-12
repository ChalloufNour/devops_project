# Stage 1: Build
FROM node:16 AS build
WORKDIR /app

COPY package*.json ./

COPY . .
RUN npm install && npm run build

RUN ls -la 
RUN ls -la dist/angular-14-crud-example

# Stage 2: Runtime
FROM nginx:alpine
COPY --from=build /app/dist/angular-14-crud-example /usr/share/nginx/html

RUN ls -la /usr/share/nginx/html 

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
