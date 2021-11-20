# Pull Docker Hub base image
FROM node:lts-alpine3.10
# Set working directory
COPY . /usr/src/myapp
WORKDIR /usr/src/myapp

# Install app dependencies
COPY package*.json ./
RUN npm install -qy

CMD ["node", "main.js"]