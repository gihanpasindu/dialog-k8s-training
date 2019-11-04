FROM nginx:1.13.3-alpine

RUN rm -rf /usr/share/nginx/html/*

ENV version=v1

RUN  echo "<h1> Serving Service $version <h1>" >> /usr/share/nginx/html/index.html

CMD ["nginx", "-g", "daemon off;"]