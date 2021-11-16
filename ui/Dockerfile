FROM node:lts-alpine as builder

WORKDIR /opt/ui

COPY . .
RUN npm config set registry https://registry.npm.taobao.org && \
    npm config set disturl https://npm.taobao.org/dist && \
    npm install && \
    npm run build

#------------------
FROM nginx

COPY --from=builder /opt/ui/dist/ /var/www
COPY nginx.conf /etc/nginx/conf.d/

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]