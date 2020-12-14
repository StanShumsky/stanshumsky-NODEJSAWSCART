FROM node:12-alpine As builder

WORKDIR /usr/share/node

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

FROM node:12.13-alpine as production

ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

WORKDIR /usr/share/node

COPY package*.json ./

RUN npm install --only=production

COPY . .

COPY --from=builder /usr/share/node/dist ./dist

ARG PORT=8080
ENV PORT=${PORT}
EXPOSE ${PORT}

CMD ["node", "dist/main"]
