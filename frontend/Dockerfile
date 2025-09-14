FROM node:24-alpine AS build
ARG NODE_OPTIONS=--openssl-legacy-provider
ENV NODE_OPTIONS=${NODE_OPTIONS}

WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build


FROM nginx:1.27-alpine
RUN rm -rf /usr/share/nginx/html && mkdir -p /usr/share/nginx/html
COPY --from=build /app/dist/frontend/ /usr/share/nginx/html

EXPOSE 80
CMD ["nginx","-g","daemon off;"]
