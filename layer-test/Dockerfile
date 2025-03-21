# FROM node:20

# Multi stage builds:

FROM node:20.18.3-alpine3.21 AS builder
WORKDIR /opt/backend
COPY package.json ./
COPY *.js ./
RUN npm install


FROM node:20.18.3-alpine3.21
# Optimizing the layers by adding mulitple instructions into one command
RUN addgroup -S expense && adduser -S expense -G expense && \
    mkdir /opt/backend && \
    chown -R expense:expense /opt/backend
ENV DB_HOST="mysql"
WORKDIR /opt/backend
USER expense
# copying the folder where all the setup files were installed in other container.
COPY --from=builder /opt/backend /opt/backend
CMD ["node", "index.js"]