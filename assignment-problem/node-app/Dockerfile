FROM node:14.17.0-slim

WORKDIR /app

COPY package.json /app

RUN npm install

COPY . .

EXPOSE 3000

CMD [ "node", "server.js" ]