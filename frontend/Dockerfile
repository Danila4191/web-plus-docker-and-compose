FROM node:18.2.0-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm ci

COPY . ./

RUN npm run build \
 && rm -rf ./src \
 && rm -rf ./node_modules 

FROM nginx:latest AS frontend
COPY --from=builder /app/build /usr/share/nginx/html
COPY nginx/conf.d/default.cong /etc/nginx/conf.d
EXPOSE 3000
CMD [ 'nginx', '-g', 'daemon off' ] 