FROM node:14.17.0-slim

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 80

# VOLUME [ "/app/feedback" ]

# CMD [ "node", "server.js" ]
# CMD ["tail", "-f", "/dev/null"]
CMD [ "npm", "start" ]