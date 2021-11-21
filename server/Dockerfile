FROM node

RUN mkdir -p /app/server
WORKDIR /app/server

COPY package.json /app/server

COPY . /app/server

RUN npm install