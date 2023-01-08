# stage 1
FROM node:latest as node
WORKDIR /app
COPY . .
RUN npm install
COPY dist/* .

# stage 2
FROM nginx:alpine
COPY --from=node /app/dist/crudtuto-Front /usr/share/nginx/html