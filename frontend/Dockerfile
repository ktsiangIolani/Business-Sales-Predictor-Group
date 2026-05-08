FROM node:20-alpine AS build

WORKDIR /app

# Copy everything first (avoids path issues)
COPY . .

# Move into frontend folder
WORKDIR /app/frontend/my-app

RUN npm install
RUN npm run build

FROM nginx:alpine

COPY --from=build /app/frontend/my-app/build /usr/share/nginx/html

RUN sed -i 's/listen       80;/listen       8080;/' /etc/nginx/conf.d/default.conf

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
