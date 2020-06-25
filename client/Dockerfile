FROM node:12.16.3-alpine as app

WORKDIR /srv/client

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build
RUN npm run export

FROM nginx

RUN rm -rf /etc/nginx/conf.d/default.conf

COPY ./nginx-conf /etc/nginx/conf.d

WORKDIR /usr/share/nginx/html

COPY  --from=app /srv/client/dist  .

EXPOSE 80
