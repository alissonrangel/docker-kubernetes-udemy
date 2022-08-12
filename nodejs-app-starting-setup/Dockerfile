FROM node:14.17.0-slim

WORKDIR /app

COPY package.json .

RUN npm install

COPY . /app

EXPOSE 80

CMD [ "node", "server.js" ]