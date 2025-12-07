FROM node:trixie-slim AS builder

WORKDIR /app

COPY ./frontend/*.json ./frontend/*lock.json ./

RUN npm install -g pnpm && \
    pnpm install --frozen-lockfile

COPY ./frontend/ . 
RUN pnpm run build

FROM nginx:latest

COPY ./frontend/nginx.conf.template /etc/nginx/templates/default.conf.template
COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80

CMD [ "nginx", "-g", "daemon off;" ]