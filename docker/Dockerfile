
# Use the Node version that matches the version you have installed locally
FROM node:18.16.0-alpine3.18
# Create app directory, in which the CAP service is built
WORKDIR /usr/src/app
# copy files
COPY app/ app/
COPY db/ db/
COPY srv/ srv/
COPY package.json db.sqlite .
# This will download and install all Node.JS dependencies and put them into the workdir/node_modules
# Install app dependencies
RUN npm install --only=production
# expose the port which is opened by CDS by default
EXPOSE 4004
# run the cap-service
CMD [ "npm", "start" ]
