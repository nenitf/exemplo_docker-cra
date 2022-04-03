FROM node:16-alpine as dev
RUN echo "DEV ENVIRONMENT"
ENV NODE_ENV development
WORKDIR /app
COPY . .
RUN yarn install

FROM node:16-alpine as prod
RUN echo "PROD ENVIRONMENT"
RUN echo "prod"
WORKDIR /app
COPY . .
RUN yarn install --frozen-lockfile
