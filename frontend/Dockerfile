FROM node:14-alpine as build

WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY . .

# Fix permissions for the node_modules binaries (including react-scripts)
RUN chmod -R 777 /app/node_modules/.bin

RUN npm run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]



