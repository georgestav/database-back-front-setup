FROM node:14

WORKDIR /app

COPY package.json /app

RUN npm install

COPY . .

ENV PORT=80
ENV MONGODB_USERNAME=root
ENV MONGODB_PASSWORD=secret

EXPOSE $PORT

CMD [ "npm", "start" ]