FROM node:16.13
RUN mkdir -p /home/node/app/
WORKDIR /home/node/app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
RUN npm install -g serve
RUN serve -s build