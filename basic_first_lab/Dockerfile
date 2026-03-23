# bad practice
FROM node:22-alpine

WORKDIR /app
COPY package*.json ./
COPY yarn.lock ./

RUN yarn install --frozen-lockfile
COPY . .
RUN yarn run build

EXPOSE 3000

CMD ["node", "dist/main.js"]

# best practice
FROM node:22-alpine3.21@sha256:db5aadf523f6cbd764bdfc1c9f53ec92e90cbd0aab9b738b49a446f1e74cdf99

RUN addgroup --system nest && \
    adduser --system nest --group nest
WORKDIR /app

COPY . .

RUN yarn install --frozen-lockfile && \
    yarn build && \
    yarn install --frozen-lockfile --production && \
    yarn cache clean

RUN chown -R nest:nest /app

USER nest
EXPOSE 3000

CMD ["node", "dist/main.js"]