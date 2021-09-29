FROM node AS app
# for small size image

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install -g npm@latest
RUN npm install express
RUN seeds/seed.js

COPY . .

EXPOSE 3000

CMD ["node", "app.js"]

##################################################################
# Lets build a multi-stage production image

FROM node:alpine

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install -g npm@latest
RUN npm install express

# This line of code does the magic to compress the image
COPY --from=app /usr/src/app /usr/src/app

EXPOSE 3000

CMD ["node", "app.js"]
